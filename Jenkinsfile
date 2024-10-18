pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                deleteDir() // Optional: Clear workspace
                git branch: 'main', url: 'https://github.com/Peh-Shin/Simple_Calculator.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Use 'sh' for Linux environment
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Build') {
            steps {
                // Build steps here
                echo 'Running calculator script...'
                sh 'python3 calculator.py 1 10 20' // Passes the operation and numbers as arguments
            }
        }

        stage('Test') {
            steps {
                // Test steps here
                script {
                    // Continue to the next stage even if tests fail
                    catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                        echo 'Running unit tests...'
                        sh 'pytest --maxfail=1 --disable-warnings'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Build and test stages completed successfully.'
        }
        failure {
            echo 'One or more stages failed. Check the logs for details.'
        }
    }
}
