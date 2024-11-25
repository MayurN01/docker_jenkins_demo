pipeline {
	agent any
	environment {
		GIT_REPOSITORY_URL = 'https://github.com/MayurN01/docker_jenkins_demo.git'
		DOCKER_IMAGE_NAME = 'mayurn01/docker_jenkins_demo'
		IMAGE_TAG = '1.0'
	}
	stages {
		stage ('Clone Repository') {
			steps {
				script {
					try {
						git branch: 'main' , url: https://github.com/MayurN01/docker_jenkins_demo.git
					} catch (Exception e) {
						echo "Failed to clone repository: ${e.message}"
						error "Failed to clone repository"
					}
				}
			}
		}

		stage('Build Docker Image') {
			steps {
				script {
					try {
						docker.build("${DOCKER_IMAGE_NAME}:${IMAGE_TAG}")
					} catch (Exception e) {
						echo "Failed to build Docker image: $(e.message}"
						error "Failed to build Docker image"
					}
				}
			}
		}

		stage('Push to DockerHub') {
			steps {
				script {
					try {
						withCredentials([usernamePassword(credentialsId: 'mayurn01', usernameVariable: 'mayurn01', passwordVariable: 'Mayur@2407')]) {
								sh """
								echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
								docker push ${DOCKER_IMAGE_NAME}:${IMAGE_TAG}
								"""
								}
							} catch (Exception e) {
								echo "Failed to push Docker image to registry: ${e.message}"
								error "Failed to push Docker image"
							}
						}
					}
				}
			}
		} 