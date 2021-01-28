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
		stage ("waiting grid") {
			steps{
				echo 'Waiting 10 seconds'
		  		sleep 10
			}
		}
		stage("Run Test"){
			steps{
				sh "docker run -e HUB_HOST=162.222.178.134 alejandrocontreras/dockerbdd"
			}
		}
	}
	post{
		always{
			sh "docker-compose down -v"
			cucumber buildStatus: 'UNSTABLE',
                            failedFeaturesNumber: 1,
                            failedScenariosNumber: 1,
                            skippedStepsNumber: 1,
                            failedStepsNumber: 1,
                            reportTitle: 'My report',
                            jsonReportDirectory: 'target/cucumber-reports/json-reports/',
                            fileIncludePattern: '**/*.json',
                            sortingMethod: 'ALPHABETICAL',
                            trendsLimit: 100
		}
	}
}