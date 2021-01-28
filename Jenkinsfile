pipeline{
	agent any
	stages{
		stage("Pull Latest Image"){
			steps{
				sh "docker pull alejandrocontreras/dockerbdd"
			}
		}
		stage("Start Grid and test"){
			steps{
				sh "docker-compose up"
			}
		}
	}
	post{
		always{
			sh "docker-compose down -v"
		}
	}
}