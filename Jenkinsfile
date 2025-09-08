pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/hamzamunir80/ecommerce-docker-site'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                bat 'docker build -t ecomsite-project .'
            }
        }

        stage('Stop Old Container') {
            steps {
                echo "Stopping old container if running..."
                bat 'docker stop ecomsite-project || echo "No container to stop"'
                bat 'docker rm ecomsite-project || echo "No container to remove"'
            }
        }

        stage('Run New Container') {
            steps {
                echo "Running new container on port 8081..."
                bat 'docker run -d -p 8081:80 --name ecomsite-project ecomsite-project'
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Website is live at http://localhost:8081/"
        }
        failure {
            echo "❌ Deployment failed. Check build logs."
        }
    }
}
