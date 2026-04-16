stage('Push Image') {
    steps {
        script {
            docker.withRegistry('https://docker.io', 'sailesh210') {
                dockerImage.push("latest")
            }
        }
    }
}
