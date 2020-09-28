pipeline {
	agent any
	tools {
		maven "maven"
	}
	stages {
		stage("Build") {
			steps {
				echo "Building Maven Project"
				sh 'mvn clean package'
				
			}
			post {
				success {
					echo "Artifact is generated succesfully"
					echo "Archiving artifact"
					archiveArtifacts artifacts: '**/*.war', followSymlinks: false
				}
				failure {
					echo "Failed to generate an artifact"
				}
			}
		
		}
		stage("Analysis") {
			steps {
				sh 'mvn checkstyle:checkstyle'
			}
			post {
				success {
					checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
				}
				failure {
					echo "Issue while  analysis"
				}
			}
		}
		stage("Deploy") {
			steps {
				deploy adapters: [tomcat9(credentialsId: '46c78b6b-09fc-463a-9692-e2925cd47b78', path: '', url: 'http://ec2-18-218-32-12.us-east-2.compute.amazonaws.com:9999/')], contextPath: null, war: '**/*.war' 
			}
			post {
				success {
					echo "Deployed successfully"
					mail bcc: '', body: 'Simple web app deployed succesfully', cc: '', from: '', replyTo: '', subject: 'Web app Deployment', to: 'pratiksrane27@gmail.com'
				}
				failure {
					echo "failure to deploy"
					mail bcc: '', body: 'Simple web app deployment failed ...please check', cc: '', from: '', replyTo: '', subject: 'Web app Deployment', to: 'pratiksrane27@gmail.com'
				}
			}
		}
	
	}
}
