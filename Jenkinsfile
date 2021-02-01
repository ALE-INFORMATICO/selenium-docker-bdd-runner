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
		stage ("waiting grid") {
			steps{
				echo 'Waiting 10 seconds'
		  		sleep 10
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
			sh "docker-compose down"
			cucumber buildStatus: 'UNSTABLE',
                            failedFeaturesNumber: 1,
                            failedScenariosNumber: 1,
                            skippedStepsNumber: 1,
                            failedStepsNumber: 1,
                            reportTitle: 'My report',
                            jsonReportDirectory: './',
                            fileIncludePattern: '**/*.json',
                            sortingMethod: 'ALPHABETICAL',
                            trendsLimit: 100
		}
	}
}
