pipeline {
    agent any
    
    stages {
        stage('Install dependencies') {
            steps {
                // Install Flask and other dependencies
                // Create virtual environment
                sh 'python3 -m venv venv'

                // Activate virtual environment (Linux/macOS)
                sh 'source venv/bin/activate'

                // Activate virtual environment (Windows)
                // bat 'venv\\Scripts\\activate'

                // Install Flask inside the virtual environment
                sh 'pip install Flask'
            }
        }
        stage('Test and Run Flask App') {
            steps {
                // Run any tests if necessary
                // You can run automated tests for your Flask app here
                
                // Run Flask app
                sh 'python hello.py &'
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
    }
}
