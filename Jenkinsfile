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
                script {
                    docker.build("flask-python-app:${BUILD_NUMBER}")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh '''
                    docker rm -f flask-app || true
                    docker run -d -p 5000:5000 --name flask-app flask-python-app:${BUILD_NUMBER}
                    '''
                }
            }
        }
    }
}
