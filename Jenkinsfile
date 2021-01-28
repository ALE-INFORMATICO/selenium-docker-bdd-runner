pipeline{
	agent any
	stages{
		stage("Pull Latest Image"){
			steps{
				sh "docker pull alejandrocontreras/dockerbdd"
			}
		}
		stage("Start Grid"){
			steps{
				sh "docker-compose up -d"
			}
		}
		stage("Run Test"){
			steps{
				sh "docker run alejandrocontreras/dockerbdd -e HUB_HOST=162.222.178.134"
			}
		}
	}
	post{
		always{
			sh "docker-compose down -v"
		}
	}
}