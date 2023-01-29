pipeline {
	agent any

	stages{
		
		stage('Build Docker Image') {
			steps {
				script {
					dockerapp = docker.build("muripalombit/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
				}
			}
		}
		
		stage ('Push Docker Image') {
			steps {
				script {
					docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
						dockerapp.push('latest')
						dockerapp.push("${env.BUILD_ID}")
					}
				}
			}
		}		
	}
}
