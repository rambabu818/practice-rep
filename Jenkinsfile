pipeline{
    agent any
    tools {
        git "git"
    }
    environment {
        PATH = "$PATH:/opt/maven/bin"
    }
    stages{
       stage('GetCode'){
            steps{
                git 'https://github.com/krishnabati/devopsmentor.git'
            }
         }        
       stage('Build'){
            steps{
                sh 'mvn clean package'
            }
         }
        stage('SonarQube analysis') {
//    def scannerHome = tool 'SonarScanner 4.0';
        steps{
        withSonarQubeEnv('sonarqube') { 
        // If you have configured more than one global server connection, you can specify its name
//      sh "${scannerHome}/bin/sonar-scanner"
        sh "mvn sonar:sonar"
    }
        }
        }
       
    }
}
