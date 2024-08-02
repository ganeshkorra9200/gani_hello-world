pipeline{
    agent any
    tools{
        maven 'maven-3.9'
    }
    stages{
        stage('checkout the code'){
            steps{
                git credentialsId: 'git_password', url: 'https://github.com/ganeshkorra9200/gani_hello-world.git'
            }
        }
        stage('build the code'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Generate sonarqube-analysis'){
            steps{
                withSonarQubeEnv('sonarqube-8') {
                 sh 'mvn sonar:sonar'
                }
            }
        }
        
		stage('Deploy War file to Tommcat'){
            steps{
               sshagent(['deploy_user']) {
                   sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ubuntu@52.91.49.77:/opt/tomcat/webapps"
				   
               }
            }
        }
    }   
 }

