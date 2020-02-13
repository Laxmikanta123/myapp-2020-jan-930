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
		stage('Upload Artifacts to Nexus'){
		nexusArtifactUploader artifacts: [
				[
					artifactId: 'myweb', 
					classifier: 'file', 
					file: 'target/myweb-pom.xml.version.war', 
					type: 'war'
				]	
			], 
			credentialsId: 'Nexus', 
			groupId: 'in.javahome', 
			nexusUrl: '15.206.159.147:8081/repository/myapp-release/', 
			nexusVersion: 'nexus3', 
			protocol: 'http', 
			repository: 'myapp-release', 
			version: 'pom.xml.version'
			}
        stage("Deploy-to-tomcat8"){
            steps{
				sshagent(['deploy-to-tomcat']) {
                    sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.11.121:/opt/tomcat8/webapps/"
                    sh "ssh ec2-user@172.31.11.121 /opt/tomcat8/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.11.121 /opt/tomcat8/bin/startup.sh"
					}
				 }
			}
			}
			}
