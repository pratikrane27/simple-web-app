pipeline {
	agent any
	tools {
		maven "maven"
	}
	stages {
		stage("Build") {
			steps {
				echo "Building Maven Project"
				#maven goal
				
			}
			post {
				success {
					echo "Artifact is generated succesfully"
					echo "Archiving artifact"
					#Artificat
				}
				failure {
					echo "Failed to generate an artifact"
				}
			}
		
		}
		stage("Analysis") {
			steps {
			
			}
			post {
				success {
					echo "SonarQube analysis is succesfull"
				}
				failure {
					echo "Issue while  analysis"
				}
			}
		}
		stage("Deploy") {
			steps {
				#deploy to tomcat 
			}
			post {
				success {
					#email notification
				}
				failure {
					echo "failure to deploy"
				}
			}
		}
	
	}
}