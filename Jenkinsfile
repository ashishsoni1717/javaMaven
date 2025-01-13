pipeline {
    agent any

    tools {
        jdk 'Java 17'
        maven 'Maven 3.9.9'
    }

    environment {
        DEPLOY_SERVER = 'your-deployment-server' // Replace with your server
        DEPLOY_USER = 'your-username' // Replace with your deployment username
        DEPLOY_PATH = '/path/to/deployment' // Replace with your deployment path
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ashishsoni1717/javaMaven.git' // Replace with your repo URL and branch
            }
        }

        stage('Setup') {
            steps {
                echo 'Setting up environment...'
                sh 'mvn clean'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn compile'
            }
        }

        stage('Unit Test') {
            steps {
                echo 'Running Unit Tests...'
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' // Report test results
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application...'
                sh 'mvn package'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.jar', fingerprint: false
                }
            }
        }

        stage('Code Quality Analysis') {
            steps {
                echo 'Running Code Quality Analysis...'
                // Example with SonarQube (optional)
                sh 'mvn sonar:sonar'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to server...'
                sh """
                    scp -o StrictHostKeyChecking=no target/*.jar ${DEPLOY_USER}@${DEPLOY_SERVER}:${DEPLOY_PATH}
                """
            }
        }
    }
        post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
    }
}