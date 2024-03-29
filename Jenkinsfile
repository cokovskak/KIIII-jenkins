pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        stage('Build image') {
            steps {
                script {
                    def app // Define app variable here
                    app = docker.build("cokovskak/kiii-jenkins")
                }
            }
        }
        stage('Push image') {
            steps {
                script {
                    def app // Define app variable here as well
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        app = docker.image("cokovskak/kiii-jenkins") // Retrieve the image
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                        // signal the orchestrator that there is a new version
                    }
                }
            }
        }
    }
}
