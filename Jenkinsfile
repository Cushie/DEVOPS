pipeline {
    agent any

    stages {
        stage('Deploy Frontend') {
            steps {
                script {
                    // Checkout frontend branch
                    checkout([$class: 'GitSCM', branches: [[name: '*/frontend']], userRemoteConfigs: [[url: 'https://github.com/Cushie/DEVOPS.git']]])

                    // Install frontend dependencies and build
                    sh 'cd frontend && npm install && npm run build'

                    // Deploy frontend to a web server (replace <Server-IP> and <Remote-Path> with your server details)
                    sh 'scp -r frontend/build/* user@<172.31.31.194>:<13.245.233.183>'
                }
            }
        }

        stage('Deploy Backend') {
            steps {
                script {
                    // Checkout backend branch
                    checkout([$class: 'GitSCM', branches: [[name: '*/backend']], userRemoteConfigs: [[url: 'https://github.com/Cushie/DEVOPS.git']]])

                    // Install backend dependencies and build
                    sh 'cd backend && npm install && npm run build'

                    // Deploy backend to a server (replace <Server-IP> and <Remote-Path> with your server details)
                    sh 'scp -r backend/dist/* user@<Server-IP>:<Remote-Path>'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
