pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vardhandeepak27/kafkaJenkins'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Run Application') {
            steps {
                bat 'java -jar target/kafkaJenkins-0.0.1-SNAPSHOT.jar &'
            }
        }

        stage('Test API') {
            steps {
                bat '''
                    curl -X POST http://localhost:8090/send -H "Content-Type: application/json" -d "Hello from Jenkins"
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}