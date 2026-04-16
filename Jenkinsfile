stage('Push Image') {
    steps {
        script {
            // Ensure 'sailesh210' matches the Credentials ID in Jenkins
            docker.withRegistry('https://docker.io', 'sailesh210') {
                dockerImage.push("latest")
            }
        }
    }
}
