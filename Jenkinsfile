pipeline {
    agent any

    environment {
        AUTH_PORT = '3132'
        CLASSROOMS_PORT = '3133'
        CLIENT_PORT = '1132'
        EVENT_BUS_PORT = '3139'
        POST_PORT = '3132'
    }

    stages {
        stage('21I-1132 - Checkout code') {
            steps {
                git 'https://github.com/NUCESFAST/scd-final-lab-exam-GitUsmanBaig'
            }
        }

        stage('21I-1132 - Build and Push Docker images') {
            steps {
                script {
                    def services = ['Auth', 'Classrooms', 'client', 'event-bus', 'Post']
                    for (service in services) {
                        dir(service) {
                            // Install dependencies
                            sh 'npm install'

                            // Build Docker image
                            def dockerImage = docker.build("i211132usman/${service}")

                            // Push Docker image
                            docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                                dockerImage.push("latest")
                            }
                        }
                    }
                }
            }
        }

        stage('21I-1132 - Test application') {
            steps {
                script {
                    // Run and test each service
                    def services = ['Auth', 'Classrooms', 'client', 'event-bus', 'Post']
                    def ports = [AUTH_PORT, CLASSROOMS_PORT, CLIENT_PORT, EVENT_BUS_PORT, POST_PORT]
                    for (int i = 0; i < services.size(); i++) {
                        sh "docker run --rm -d -p ${ports[i]}:${ports[i]} --name ${services[i]} i211132usman/${services[i]}"
                         // Give the app some time to start
                        sh 'sleep 5'
                        sh "curl localhost:${ports[i]}"
                        sh "docker stop ${services[i]}"
                    }
                }
            }
        }
    }
}