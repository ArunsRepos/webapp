pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "Maven3"
    }

    stages {
        stage('Get Source Code') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/ArunsRepos/webapp.git'

                

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
            
        }
        
            stage('Build') {
            steps {
                    
                sh '''  mvn clean install'''
            
            }
            }

            stage('Archive') {
            steps {
                    
                sh '''  cd /home/ec2-user/jenkins/jenkins/workspace/Build
                        mkdir -p versions
                        cp target/my-app.war versions/my-app-V$BUILD_ID.war'''
            
            }
            }

            stage('Notification') {
            steps {
              
                    slackSend color: "green", message: "Build Started: ${env.JOB_NAME} ${env.BUILD_NUMBER}"           
            }
            }
    }
}

