pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Check out code from Git repository
                git url: 'https://github.com/yourusername/your-maven-project.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Run Maven build
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                // Run Maven tests
                sh 'mvn test'
            }
        }
    }

    post {
        always {
            // Archive test reports even if tests fail
            junit '**/target/surefire-reports/*.xml'
        }
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}
