pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '"mvn" -Dmaven.test.failure.ignore clean install'
      }
    }
    stage('Deploy') {
      steps {   
         deploy adapters: [tomcat8(credentialsId: 'Deploy', path: '', url: 'http://65.1.64.115:8080')], contextPath: null, war: '**/**.war'
      }
    }
  }
}
