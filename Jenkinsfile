pipeline{
    agent none
    stages {

          stage("Test"){
        agent {
                label 'krishna_personal_system'
            }

            steps{
                bat "mvn clean test" 
            }
        }
}
}
