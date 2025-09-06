pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Ericliu-uz/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
            post {
                always {
                    emailext (
                        subject: "Test Stage Completed - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        to: "your-email@outlook.com",
                        body: "Test stage has completed with status: ${currentBuild.currentResult}",
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
            post {
                always {
                    emailext (
                        subject: "Security Scan Completed - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        to: "your-email@outlook.com",
                        body: "Security scan stage has completed with status: ${currentBuild.currentResult}",
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }
    }
}