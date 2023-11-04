pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/arun0208/ToDo-List.git'
            }
        }
        
        stage('Build and Test') {
            steps {
                sh 'npm install'
                sh 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('todolist:dev')
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image('todolist:dev').push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful. Trigger your production deployment here.'
            // Implement your deployment to production here (e.g., using Kubernetes, Docker Swarm, etc.)
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
