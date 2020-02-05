pipeline{
	agent any
	 tools {
        maven 'mvn3'
    }
	
	stages(from git){
		stage{
			steps{
			git credentialsId: 'Laxmikanta123', 
			url: 'https://github.com/Laxmikanta123/myapp-2020-jan-930'
			}
		}
		}
		stages(maven){
		stage{
			steps{
			sh label: '', script: 'mvn clean package'
			}
		}
		}

}
