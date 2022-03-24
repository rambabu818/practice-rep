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
  -Dsonar.host.url=http://54.145.60.38:9000 \
  -Dsonar.login=sonaserver_key"
              }
        }
        stage("Upload to Nexus"){
            when {
                branch 'main'
            }
            steps{
            nexusPublisher nexusInstanceId: 'javanexusrepo', nexusRepositoryId: 'javanexusrepo', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '**/*.war']], mavenCoordinate: [artifactId: '${POM_ARTIFACTID}', groupId: '${POM_GROUPID}', packaging: 'war', version: '${POM_VERSION}']]]            }
        }

        stage("Deploy to dev and test"){
            when {
                branch 'main'
            }
            steps{
                sh 'wget --user=admin --password=admin@123 http://54.234.40.160:8081/repository/javanexusrepo/com/devops-mentors/javaproject/${POM_VERSION}/${POM_ARTIFACTID}-${POM_VERSION}.war'
               deploy adapters: [tomcat9(credentialsId: 'tomactdeployer_logindetails', path: '', url: 'http://18.207.120.230:8080/')], contextPath: null, war: '**/*.war'
            }
        }
        
      
    }
}
