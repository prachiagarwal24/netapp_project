pipeline {
    agent any
        
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
                    sh 'sudo docker build -t my-flask-app_jenkins .'
                    sh 'sudo docker tag my-flask-app_jenkins prachi24oracle/my-flask-app_jenkins:latest'
                    sh 'sudo docker login -u prachi24oracle -p sl28@Prachi'
                    sh 'sudo docker push prachi24oracle/my-flask-app_jenkins:latest'           
                }
            }
        }
    }
}
