pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
        git "git"
    }

    stages {
        
        stage('get source code') {
            steps {
                                git 'https://github.com/krishnabati/devopsmentor.git'
 
            }
        }
       
        stage('Build') {
            steps {
                // Get some code from a GitHub repository

                // Run Maven on a Unix agent.
                // sh "mvn -Dmaven.test.failure.ignore=true clean package"
                    sh "mvn clean package sonar:sonar"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

        
        }
    }
}
