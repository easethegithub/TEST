pipeline {
    agent any

    environment {
        JAVA_HOME = 'C:\\Program Files\\Java\\jdk-21'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from Git repository
                git url: 'https://github.com/easethegithub/TEST.git', branch: 'main'
            }
        }
        
        stage('Build') {
            steps {
                script {
                    // Compile the Java program using javac
                    sh 'javac HelloWorld.java'
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // In a real-world scenario, you would run unit tests here
                    // Since this is a simple HelloWorld program, we just print the message
                    echo 'Running tests... (in this case, just printing HelloWorld)'
                }
            }
        }

        stage('Package') {
            steps {
                script {
                    // Optionally, you could package the application as a JAR
                    // If you're using Maven or Gradle, this is where you'd run them.
                    // For simplicity, we're not packaging the JAR here
                }
            }
        }

        stage('Docker Build and Push') {
            steps {
                script {
                    // Use Jenkins credentials for Docker Hub login
                    withCredentials([usernamePassword(credentialsId: '2908b623-6530-48b5-b890-222c2a591b15', usernameVariable: 'vaibhavdock77', passwordVariable: 'Vaibhav@123')]) {
                        // Login to Docker Hub
                        sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin"

                        // Build Docker image
                        sh 'docker build -t my-docker-image .'

                        // Push Docker image to Docker Hub
                        sh 'docker push my-docker-image'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Run the Java program
                    sh 'java HelloWorld'
                }
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Something went wrong with the build or deployment.'
        }
    }
}
