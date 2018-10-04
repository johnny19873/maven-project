pipeline {
  agent none
  stages {
    stage('Compilar') {
      parallel {
        stage('Compilar') {
          agent {
            node {
              label 'ubuntu'
            }

          }
          steps {
            sh 'mvn clean package'
            archiveArtifacts(artifacts: '**/*.war', fingerprint: true, onlyIfSuccessful: true)
          }
        }
        stage('CheckStyle') {
          agent {
            node {
              label 'ubuntu'
            }

          }
          steps {
            sh 'mvn checkstyle:checkstyle'
            checkstyle()
          }
        }
      }
    }
    stage('Aprobar') {
      agent {
        node {
          label 'Windows'
        }

      }
      steps {
        input(message: 'Deseas aprobar el despliegue?', ok: 'Si', id: '123456')
      }
    }
    stage('Despliegue') {
      agent {
        node {
          label 'Windows'
        }

      }
      steps {
        copyArtifacts(projectName: 'maven-project', fingerprintArtifacts: true, flatten: true)
      }
    }
  }
  environment {
    TOMCAT_HOME = 'C:\\Tomcat_8.5\\webapps'
  }
}