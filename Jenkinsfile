pipeline {
    environment {
        DOCKER_CONFIG = "${env.WORKSPACE}/.docker"
    }
    
    agent {
        docker {
            image 'docker:20.10.7'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/CHARIF-SANTIPET/jenkins-demo-app.git'
            }
        }
        stage('Build Image') {
            steps {
                sh '''
                    mkdir -p $DOCKER_CONFIG
                    docker build -t jenkins-demo-app:latest .
                '''
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
                sh 'pytest || true'
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8081:8081 --name demo-app jenkins-demo-app:latest'
            }
        }
        

    }
}
