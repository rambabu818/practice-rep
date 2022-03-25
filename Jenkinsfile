pipeline{
    agent any
    tools {
        maven 'maven'
        jdk "java11"
    }
    stages {

        stage("pull SCM"){
            steps{
            git branch: 'main', url: 'https://github.com/krishnabati/devopsmentor.git'   
               }
        }
         stage("Test"){
           
            steps{
                sh "mvn clean test" 
            }
        }

        stage("Build"){
           
            steps{
                sh "mvn clean install" 
            }
        }

        stage("Code Analysis by Sonar"){
            
            steps{
                
           sh "mvn sonar:sonar \
  -Dsonar.projectKey=newproject \
  -Dsonar.host.url=http://54.90.55.79:9000 \
  -Dsonar.login=e11192779c15acb4f5a7c8a0199c8d6c2c55f82f"
              }
        }
        stage("Upload to Nexus"){
           
            steps{
nexusPublisher nexusInstanceId: 'javanexusrepo', nexusRepositoryId: 'javanexusrepo', packages: [[$class: 'MavenPackage', mavenAssetList: [], mavenCoordinate: [artifactId: 'javaproject', groupId: 'com.devops-mentors', packaging: 'war', version: '1.35']]]
        }

        }
        stage("Pull Artifact"){
           
            steps{
                sh "wget --user=admin --password=admin@123 http://18.212.203.160:8081/repository/javanexusrepo/com/devops-mentors/javaproject/1.35/javaproject-1.35.war"
            }
        }
        
          stage("deploy to Server"){
           
            steps{
deploy adapters: [tomcat9(credentialsId: 'tomactdeployer_logindetails', path: '', url: 'http://54.175.5.117:8080/')], contextPath: null, war: '**/*.war'            }
        }
    }
}
