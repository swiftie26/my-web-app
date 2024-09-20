pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    echo "Building the application..."
                    sh 'npm install'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    echo "Running tests..."
                    sh 'npm test'
                }
            }
        }
        stage('Code Quality Analysis') {
            steps {
                script {
                    echo "Running ESLint..."
                    sh 'npm run lint'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo "Building Docker image..."
                    // Build the Docker image with your DockerHub username
                    sh 'docker build -t <your-dockerhub-username>/my-web-app:latest .'
                    
                    echo "Running Docker container in staging..."
                    // Run the Docker container on port 3000
                    sh 'docker run -d -p 3000:3000 <ayesharana4>/my-web-app:latest'
                }
            }
        }
        stage('Release') {
            steps {
                script {
                    echo "Deploying to Production..."
                    // Log in to DockerHub and push the image
                    withCredentials([ayesh(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKERHUB_USER', passwordVariable: 'DOCKERHUB_PASS')]) {
                        sh 'docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASS'
                        sh 'docker push <ayesharana4>/my-web-app:latest'
                    }
                }
            }
        }
    }
}
