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
				sh "docker-compose up -d selenium-event-bus selenium-sessions selenium-session-queuer selenium-distributor selenium-router chrome firefox"
			}
		}
		stage("Run Test"){
			steps{
				sh "docker-compose up dockerbdd"
			}
		}
	}
	post{
		always{
			sh "docker-compose down -v"
		}
	}
}