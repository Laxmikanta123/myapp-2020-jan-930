pipeline{
    agent any
    tools {
        maven 'mvn3'
    }
    stages{
        stage('Maven Build'){
            steps{
                sh script: 'mvn clean package'
            }
        }
        stage("Deploy-to-tomcat8"){
            steps{
				sshagent(['deploy-to-tomcat']) {
                    sh "scp -o StrictHostKeyChecking=no target/myweb*.war ec2-user@172.31.40.148:/opt/tomcat8/webapps/myweb.war"
                    sh "ssh ec2-user@172.31.40.148 /opt/tomcat8/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.40.148 /opt/tomcat8/bin/startup.sh"
					}
				 }
			}
			}
			}
