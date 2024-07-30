pipeline {
    agent any

    triggers {
        cron('0 0 * * *') // Runs the job every day at midnight
    }

    environment {
        AWS_CREDENTIALS_ID = 'aws-credentials-id' // Replace with your AWS credentials ID in Jenkins
        AWS_REGION = 'us-east-1' // Replace with your desired AWS region
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository
                cleanWs()
                checkout scm
            }
        }

        stage('Setup Environment') {
            steps {
                script {
                    // Setup Python virtual environment and install dependencies
                    sh '''
                    python3 -m venv venv
                    source venv/bin/activate
                    pip install -r requirements.txt
                    '''
                }
            }
        }

        stage('Run Script with AWS Credentials') {
            steps {
                withAWS(credentials: "${AWS_CREDENTIALS_ID}", region: "${AWS_REGION}") {
                    script {
                        // Run the Python script with AWS credentials
                        sh '''
                        source venv/bin/activate
                        python my_script.py
                        '''
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                // Clean up: Deactivate virtual environment and remove it
                sh '''
                deactivate || true
                rm -rf venv
                '''
            }
        }
        failure {
            echo 'Pipeline failed!'
        }
        success {
            echo 'Pipeline succeeded!'
        }
    }
}