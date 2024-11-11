pipeline {
    agent any

    environment {
        // Define Docker credentials as environment variables
        DOCKER_USERNAME = 'vaibhavdock77' // Replace with your Docker Hub username
        DOCKER_PASSWORD = 'Vaibhav@123' // Replace with your Docker Hub password
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

                    // Login to Docker Hub using environment variables (Windows uses bat)
                    bat """
                        echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin
                    """
                    
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
