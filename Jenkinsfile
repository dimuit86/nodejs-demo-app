pipeline {
	environment {
		registry = "dimuit86/nodejs-demo-app"
		registryCredential = 'dockerhub_id'
		dockerImage = ''
	}
	agent any
	stages {
		stage('Cloning our Git') {
			steps {
				git 'https://github.com/dimuit86/nodejs-demo-app.git'
			}
		}


		stage('Code Quality Check via SonarQube') {
			steps {
				script {
				def scannerHome = tool 'SonarqubeScanner';
					withSonarQubeEnv("SonarqubeServer") {
					sh "${scannerHome}/bin/sonar-scanner \
						-Dsonar.projectKey=nodejs-demoapp \
						-Dsonar.sources=. \
						-Dsonar.css.node=. \
						-Dsonar.host.url=http://viqsonar.eastus.cloudapp.azure.com:9000/ \
						-Dsonar.login=squ_3ef641a03e8177d7a0ef638f69fafc2414d15a59"
					}

				}
			}
		}

		
		// stage('SonarQube analysis') {
		// 	steps {
		// 		script {
		// 		// requires SonarQube Scanner 2.8+
		// 		scannerHome = tool 'SonarqubeScanner'
		// 		}
		// 		withSonarQubeEnv('SonarqubeServer') {
		// 		sh "${scannerHome}/bin/sonar-scanner"
		// 		}
		// 	}
		// }

		stage('Building our image') {
			steps {
				script {
					dockerImage = docker.build registry + ":$BUILD_NUMBER"
				}
			}
		}
		stage('Deploy our image') {
			steps {
				script {
					docker.withRegistry('', registryCredential) {
						dockerImage.push()
					}
				}
			}
		}
		stage('Cleaning up') {
			steps {
				sh "docker rmi $registry:$BUILD_NUMBER"
			}
		}
	}
}