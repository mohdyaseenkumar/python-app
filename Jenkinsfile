pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/mohdyaseenkumar/python-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t flask-python-app:${BUILD_NUMBER} .
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f flask-app || true
                docker run -d -p 5000:5000 --name flask-app flask-python-app:${BUILD_NUMBER}
                '''
            }
        }
    }
}
