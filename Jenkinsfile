pipeline {
    agent {
       node {
	  label 'master'
            }
	  }
    options{
	timestamps()
	}
	
    stages{
	stage("Checkout, Verify") {
         steps{
           checkout scm			
         script{
           sh(/mvn clean verify/)
	    }		
// step([$class : 'Publisher', reportFilenamePattern : '**/testng-results.xml'])
        }
}
		
       stage("Email"){
	  steps{
	    emailext (to: 'ayankbiswas@gmail.com', replyTo: 'ayankbiswas@gmail.com', subject: "Email Report from - '${env.JOB_NAME}' ", body: readFile("target/cucumber.html"), mimeType: 'text/html');
	}
     }
   }
}
