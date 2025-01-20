pipeline {
    agent any

    // tools {
    //     jdk 'JDK 17'          // Specify the JDK version installed on Jenkins
    //     maven 'Maven 3.9.9'   // Specify the Maven version installed on Jenkins
    // }

    environment {
        DEPLOY_ENV = 'staging' // Example deployment environment
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                git branch: 'master', url: 'https://github.com/ashishsoni1717/javaMaven.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh """
                # Example: SCP deployment
                scp target/your-app.jar user@server:/path/to/deploy/
                ssh user@server "java -jar /path/to/deploy/your-app.jar"
                """
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Pipeline succeeded.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
