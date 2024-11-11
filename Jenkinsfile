pipeline {
    agent any

    environment {
        // Docker username and password will be injected using withCredentials
        DOCKER_USERNAME = 'sutarvaibhavv77@gmail.com'  // Leave blank, will be set by Jenkins credentials
        DOCKER_PASSWORD = 'Vaibhav@123'  // Leave blank, will be set by Jenkins credentials
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from Git repository
                git url: 'https://github.com/easethegithub/TEST.git', branch: 'main'
            }
        }

        stage('Build Java Program') {
            steps {
                script {
                    // Compile the Java program using javac (Windows uses bat)
                    bat 'javac HelloWorld.java'
                }
            }
        }

        stage('Test Java Program') {
            steps {
                script {
                    // Run the Java program (Windows uses bat)
                    bat 'java HelloWorld'
                }
            }
        }

        stage('Docker Build and Push') {
            steps {
                script {
                    // Ensure Docker is installed (Windows uses bat)
                    bat 'docker --version'

                    // Use Jenkins credentials to securely login to Docker Hub
                    withCredentials([usernamePassword(credentialsId: '2908b623-6530-48b5-b890-222c2a591b15', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        // Login to Docker Hub using environment variables
                        bat """
                            echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin
                        """
                    }

                    // Build Docker image (Windows uses bat)
                    bat 'docker build -t my-docker-image .'

                    // Push Docker image to Docker Hub (Windows uses bat)
                    bat 'docker push my-docker-image'
                }
            }
        }
    }

    post {
        success {
            echo 'Java build, test, Docker image build, and push were successful!'
        }
        failure {
            echo 'Something went wrong during the build or Docker process.'
        }
    }
}
