pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'kolevas/kiii_repo'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building the application..."'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
                // Add test commands here
            }
        }

        stage('Docker Build and Push') {
            when {
                branch 'dev'
            }
            steps {
                sh 'echo "Building and pushing Docker image..."'
                sh 'docker build -t $DOCKER_IMAGE:latest .'
                sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'
                sh 'docker push $DOCKER_IMAGE:latest'
            }
        }
    }

    post {
        always {
            sh 'echo "Pipeline execution complete."'
        }
    }
}
