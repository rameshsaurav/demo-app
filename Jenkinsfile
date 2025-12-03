pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/rameshsaurav/demo-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo Building application...'
                sh 'npm install'   // or mvn package / pip install
            }
        }

        stage('Test') {
            steps {
                sh 'echo Running tests...'
                sh 'npm test'      // or pytest / mvn test
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo Deploying application...'
                // Example: Docker deploy
                sh '''
                docker build -t webapp .
                docker stop webapp || true
                docker rm webapp || true
                docker run -d --name webapp -p 8080:8080 webapp
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
