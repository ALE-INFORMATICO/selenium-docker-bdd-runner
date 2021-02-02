pipeline{
	agent any
	stages{
		stage("Pull Latest Image"){
			steps{
				sh "docker-compose down -v"
				sh "rm -r output/ volume/"
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
			sh "pwd"
			sh "ls -al"
			cucumber buildStatus: 'UNSTABLE',
                            failedFeaturesNumber: 1,
                            failedScenariosNumber: 1,
                            skippedStepsNumber: 1,
                            failedStepsNumber: 1,
                            reportTitle: 'Reporte personalizado',
                            jsonReportDirectory: '/home/test24122020/jenkins/workspace/test_runner',
                            fileIncludePattern: '**/*.json',
                            sortingMethod: 'ALPHABETICAL',
                            trendsLimit: 100
		}
	}
}
