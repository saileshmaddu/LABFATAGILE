pipeline {
    agent any
    environment {
        // MUST match your Docker Hub username/repo
        DOCKER_IMAGE = "saileshmaddu/html-demo" 
        // MUST match the ID you created in Jenkins Credentials
        DOCKER_CREDS_ID = "dockerhub" 
    }
    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/saileshmaddu/LABFATAGILE.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                // We use 'bat' because you are on Windows
                bat "docker build -t %DOCKER_IMAGE%:latest ."
            }
        }
        stage('Push Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "$sailesh210", usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                        // Log in and push using the credentials
                        bat "docker login -u %USER% -p %PASS%"
                        bat "docker push %DOCKER_IMAGE%:latest"
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                // Ensure 'kubeconfig' is a 'Secret File' in Jenkins credentials
                withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG')]) {
                    bat "kubectl --kubeconfig=%KUBECONFIG% apply -f deployment.yaml"
                }
            }
        }
    }
}
