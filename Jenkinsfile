pipeline{
    agent none
    stages {

          stage("Test"){
        agent {
                label 'java_project_label'
            }

            steps{
                bat "mvn clean test" 
            }
        }
}
}
