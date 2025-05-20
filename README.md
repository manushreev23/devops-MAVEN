pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // Run Maven build
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                // Run tests
                sh 'mvn test'
            }
        }
    }
    post {
        always {
            // Archive test reports
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
