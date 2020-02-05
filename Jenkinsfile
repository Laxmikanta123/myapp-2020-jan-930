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

		  }
    stages{
        stage('deploy to tomcat8'){
            steps{
                deploy adapters: [tomcat8(credentialsId: 'tomcat_manager', path: '', url: 'http://172.31.6.219:8080/')], contextPath: '/opt/tomcat8/webapps/myweb.war', war: 'target/*.war'
            }
        }

		  }
		}
