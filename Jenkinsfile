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
                    sh 'npm test' // You can implement your own test script in package.json
                }
            }
        }
        stage('Code Quality Analysis') {
            steps {
                script {
                    echo "Running SonarQube analysis..."
                    // Assume you have SonarQube configured in Jenkins
                    withSonarQubeEnv('SonarQube') {
                        sh 'sonar-scanner'
                    }
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo "Deploying to Staging..."
                    sh 'docker build -t my-web-app .'
                    sh 'docker run -d -p 3000:3000 my-web-app'
                }
            }
        }
        stage('Release') {
            steps {
                script {
                    echo "Deploying to Production..."
                    // Use your release management tool here (e.g., AWS, Octopus Deploy)
                    sh 'docker push my-web-app:latest'  // Assuming DockerHub or any registry
                }
            }
        }
    }
}
