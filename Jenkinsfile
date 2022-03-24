pipeline{
    agent any
    tools {
        maven 'maven'
        jdk "java11"
    }
    stages {

        stage("SCM"){
            steps{
            git branch: 'main', url: 'https://github.com/krishnabati/devopsmentor.git'   
               }
        }
        stage("Maven Build"){
           
            steps{
                sh "mvn clean install" 
            }
        }

        stage("Sonar Analysis"){
            
            steps{
                
           sh "mvn sonar:sonar \
  -Dsonar.projectKey=newproject \
  -Dsonar.host.url=http://54.198.220.207:9000 \
  -Dsonar.login=e11192779c15acb4f5a7c8a0199c8d6c2c55f82f"
              }
        }
        stage("Upload to Nexus"){
            // when {
            //     branch 'main'
            // }
            steps{
            nexusPublisher nexusInstanceId: 'javanexusrepo', nexusRepositoryId: 'javanexusrepo', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/var/lib/jenkins/workspace/newpipeline/app/target/app.war']], mavenCoordinate: [artifactId: 'javaproject', groupId: 'com.devops-mentors', packaging: 'war', version: '1.32']]]            }
        }

        stage("Deploy to dev and test"){
            // when {
            //     branch 'main'
            // }
            steps{
                sh 'wget --user=admin --password=admin@123 http://54.234.40.160:8081/repository/javanexusrepo/com/devops-mentors/javaproject/1.32/javaproject-1.32.war'
               deploy adapters: [tomcat9(credentialsId: 'tomactdeployer_logindetails', path: '', url: 'http://18.207.120.230:8080/')], contextPath: null, war: '/var/lib/jenkins/workspace/newpipeline/app/target/app.war'
            }
        }
        
      
    }
}
