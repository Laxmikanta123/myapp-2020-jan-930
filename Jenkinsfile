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
		steps{
			script {
               def pomFile = readMavenPom file: 'pom.xml'
               def nexusRepo = "myapp-release"
               if(pomFile.version.endsWith("SNAPSHOT")){
					nexusRepo = "myapp-snapshot"
					}
					nexusArtifactUploader artifacts: [
						[
							artifactId: 'myweb', 
							classifier: 'file', 
							file: "target/myweb-${pomFile.version}.war", 
							type: 'war'
						]	
					], 
					credentialsId: 'Nexus', 
					groupId: 'in.javahome', 
					nexusUrl: '15.206.159.147:8081/repository/maven-snapshots/', 
					nexusVersion: 'nexus3', 
					protocol: 'http', 
					repository: 'myapp-release', 
					version: "${pomFile.version}"
			}
			}
			}
        stage("Deploy-to-tomcat8"){
            steps{
				sshagent(['deploy-to-tomcat']) {
                    sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.40.148:/opt/tomcat8/webapps/"
                    sh "ssh ec2-user@172.31.40.148 /opt/tomcat8/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.40.148 /opt/tomcat8/bin/startup.sh"
					}
				 }
			}
			}
			}
