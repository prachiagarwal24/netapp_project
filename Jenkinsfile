pipeline {
    agent any
        
    environment {
        DOCKER_HUB_USERNAME = credentials('prachi24oracle')
        DOCKER_HUB_PASSWORD = credentials('sl28@Prachi')
        DOCKER_HUB_REPO = 'prachi24oracle/my-flask-app_jenkins' // Replace with your Docker Hub repository name
        DOCKER_IMAGE_TAG = 'latest'
    }
    stages {

        stage('Install dependencies') {
            steps {
                // Install Flask inside the virtual environment
                sh 'sudo apt-get install python3-flask'
            }
        }
        stage('Test and Run Flask App') {
            steps {
                // Run any tests if necessary
                // You can run automated tests for your Flask app here
                
                // Run Flask app
                sh 'python3 hello.py &'
                // & at the end to run Flask app in background
            }
        }
        stage('Verify Flask App') {
            steps {
                // Perform any verification steps here (optional)
                // You can use curl or any other tool to make HTTP requests and verify the response
                sh 'sleep 5' // Wait for the Flask app to start (adjust as needed)
                sh 'curl http://localhost:5000' // Send a request to the Flask app
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Build Docker image using Dockerfile
                script {
                    docker.build("${DOCKER_HUB_REPO}:${DOCKER_IMAGE_TAG}", '.')
                }
            }
        }
        stage('Log in to Docker Hub') {
            steps {
                // Log in to Docker Hub
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_USERNAME, DOCKER_HUB_PASSWORD) {
                        // Push Docker image to Docker Hub
                        docker.image("${DOCKER_HUB_REPO}:${DOCKER_IMAGE_TAG}").push()
                    }
                }
            }
        }
    }
}
