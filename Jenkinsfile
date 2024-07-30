pipeline {
    agent any

    triggers {
        // cron('0 0 * * *') // Runs the job every day at midnight
        cron('*/5 * * * *') // Every 5 minutes
    }

    environment {
        AWS_CREDENTIALS_ID = 'aws-credentials-id' // Replace with your AWS credentials ID in Jenkins
        AWS_REGION = 'us-east-1' // Replace with your desired AWS region
        INSTALL_DONE = '' // Initialize the variable
        SETUP_FILE = 'setup_done.txt' // File to track setup status
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
        // when {
        //         expression {
        //             // Only execute if INSTALL_DONE is not set
        //                //return env.INSTALL_DONE == '' 
        //              return !fileExists(env.SETUP_FILE)
        //         }
        // }
        
      steps {
          script {
            // Upgrade pip and install dependencies
            // sh '''
            // python3 --version
            // which python3
            // python3 -m pip list
            // python3 -m pip install --upgrade pip
            // python3 -m pip install requests boto3
            // '''
            // // Mark installation as done
            // //env.INSTALL_DONE = 'done'
            // sh 'touch ${SETUP_FILE}'

              def setupFile = 'install_done.txt'
              def setupDone = fileExists(setupFile)
                echo "Setup done: ${setupDone}"
                if (!setupDone) {
                        // Upgrade pip and install dependencies
                        sh '''
                        python3 --version
                        which python3
                        python3 -m pip list
                        python3 -m pip install --upgrade pip
                        python3 -m pip install requests boto3
                        '''
                        // Mark installation as done
                        writeFile file: setupFile, text: 'done'
                       echo 'Installing setup.'
                    } else {
                        echo 'Environment setup already done.'
                    }
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
