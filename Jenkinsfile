pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Setup Environment') {
            steps {
                script {
                    // Check if running on Unix (Linux/Mac) or Windows
                    if (isUnix()) {
                        sh 'python3 -m venv venv'
                        sh '. venv/bin/activate && pip install pytest'
                    } else {
                        bat 'python -m venv venv'
                        bat 'venv\\Scripts\\activate.bat && pip install pytest'
                    }
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    if (isUnix()) {
                        // Activate venv and run tests
                        // Note: Using test_baitap1.py as test_main.py was not found
                        sh '. venv/bin/activate && pytest test_baitap1.py'
                    } else {
                        // Activate venv and run tests
                        bat 'venv\\Scripts\\activate.bat && pytest test_baitap1.py'
                    }
                }
            }
        }
    }
}
