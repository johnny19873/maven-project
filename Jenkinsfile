pipeline {
  agent none
  stages {
    stage('Compilar') {
      parallel {
        stage('Compilar') {
          steps {
            sh 'mvn clean package'
            archiveArtifacts(artifacts: '**/*.war', fingerprint: true, onlyIfSuccessful: true)
          }
        }
        stage('CheckStyle') {
          steps {
            sh 'mvn checkstyle:checkstyle'
            checkstyle()
          }
        }
      }
    }
    stage('Aprobar') {
      steps {
        input 'asassas'
      }
    }
    stage('Despliegue') {
      steps {
        copyArtifacts(projectName: 'maven-project', fingerprintArtifacts: true, flatten: true)
      }
    }
  }
  environment {
    TOMCAT_HOME = 'C:\\Tomcat_8.5\\webapps'
  }
}