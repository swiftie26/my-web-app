pipeline {
    agent any
    
    tools {
        nodejs 'NodeJS 14'  // The name you set for NodeJS in the previous step
    }

    stages {
        stage('Build') {
            steps {
                git 'https://github.com/swiftie26/my-web-app.git'
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
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
