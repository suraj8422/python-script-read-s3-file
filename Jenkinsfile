pipeline {
    agent any

    triggers {
        // cron('0 0 * * *') // Runs the job every day at midnight
        cron('*/10 * * * *') // Every 5 minutes
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
            Upgrade pip and install dependencies
            sh '''
            python3 --version
            which python3
            python3 -m pip install --upgrade pip
            python3 -m pip install requests boto3
            '''
         }
     }
  }

        // stage('Setup Environment') {
        //     steps {
        //         script {
        //             // Setup Python virtual environment and install dependencies
        //             sh '''
        //             python3 -m venv venv
        //             source venv/bin/activate
        //             pip install requests boto3
        //             '''
        //         }
        //     }
        // }

        // stage('Run Script with AWS Credentials') {
        //     steps {
        //         withAWS(credentials: "${AWS_CREDENTIALS_ID}", region: "${AWS_REGION}") {
        //             script {
        //                 // Run the Python script with AWS credentials
        //                 sh '''
        //                 source venv/bin/activate
        //                 python my_script.py
        //                 '''
        //             }
        //         }
        //     }
        // }
        
    }
}
