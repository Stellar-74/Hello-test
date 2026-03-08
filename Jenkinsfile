pipeline {
    agent any

    stages {
        stage('Checkout & Run') {
            steps {
                // Pull code from GitHub
                checkout scm

                // Run the Python script
                sh 'python3 index.py'
            }
        }
    }
}
