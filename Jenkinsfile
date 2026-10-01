pipeline {
	agent any

	environment {
		CONTAINER_NAME = "nestjs-app"
		IMAGE_NAME = "nesths-image"
		EMAIL = "prajyotbhagat1989@gmail.com"
		PORT = "3000"
	}

	stages {
		stage('Clone Repo') {
			steps {
				git branch: 'main',
				url: 'https://github.com/prajyotbhagat/demo-project-jenkins-docker'
			}
		}
		stage('Build Docker Image') {
			steps {
				sh 'docker build -t $IMAGE_NAME'
			}
		}
		stage('Stop and Remove Previous Container') {
                        steps {
                                sh """
					docker stop $CONTAINER_NAME || true
					docker rm $CONTAINER_NAME || true
				"""
                        }
                }
		stage('Docker Container Run') {
                        steps {
                                sh """
					docker run -d -p ${PORT}:${PORT}
					--name $CONTAINER_NAME $IMAGE_NAME
				"""
                        }
                }
		stage('Send Email Notification') {
                        steps {
				emailtext(
					subject: "NestJS App Deployed Successfully on EC2!",
					body: "Your Nest JS app is deployed http://54.221.79.132:3000/",
					to: "${EMAIL}"
                        }
                }
	}
}
