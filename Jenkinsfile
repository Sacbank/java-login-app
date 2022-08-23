pipeline{
    agent any
    environment {
        PATH = "$PATH:/usr/share/maven/bin"
    }
    stages{
       stage('GetCode'){
            steps{
                git 'https://github.com/Sacbank/java-login-app.git'
            }
         }        
       stage('Build'){
            steps{
                sh 'mvn clean package'
            }
         }
        stage('Test'){
            steps{
                sh 'mvn test'
            }
            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
         }
		stage('SonarQube analysis') {
//    def scannerHome = tool 'SonarScanner 4.0.0';
        steps{
        withSonarQubeEnv('sonarqube-8.9.9') { 
        // If you have configured more than one global server connection, you can specify its name
//      sh "${scannerHome}/bin/sonar-scanner"
        sh "mvn sonar:sonar"
    }
        }
        }
         stage('Deploy') {
      steps {   
         deploy adapters: [tomcat8(credentialsId: 'Deploy', path: '', url: 'http://3.110.62.208:8080')], contextPath: null, war: '**/**.war'
    }
    }
       
    }
}

