pipeline{
    agent none
    stages {

          stage("Test"){
        agent {
                label 'Ram_personal_system'
            }

            steps{
                bat "mvn clean test" 
            }
        }
}
}
