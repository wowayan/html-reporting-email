pipeline {
	agent {
		node {
			label 'main'
		}
	}
	
	options{
		timestamps()
	}
	
	
	stages{
		stage("Checkout, Test & Publish") {
			steps{
				checkout scm
				
				script{
					sh(/mvn clean test /)
				}
				
				// step([$class : 'Publisher', reportFilenamePattern : '**/testng-results.xml'])
			}
		}
		stage('Archive Cucumber Json Report') {
                          archiveArtifacts artifacts: 'target/cucumber*', fingerprint: true, followSymlinks: false
                      }
                        stage('Generate Cucumber HTML reports') {
                                cucumber buildStatus: 'UNSTABLE',
                                fileIncludePattern: 'cucumber*.json',
                                hideEmptyHooks: true,
                                jsonReportDirectory: 'target'
                            }
		
		stage("Email"){
			steps{
				emailext (to: 'ayankbiswas@gmail.com', replyTo: 'ayankbiswas@gmail.com', subject: "Email Report from - '${env.JOB_NAME}' ", body: readFile("target/surefire-reports/emailable-report.html"), mimeType: 'text/html');
			}
		}
	}
	

}
