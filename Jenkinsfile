pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    def version = sh(script: 'echo $BUILD_NUMBER', returnStdout: true).trim()
                    def dockerImage = "djangoapp:${version}"
                    
                    // Build and tag the Docker image
                    sh "docker build -t ${dockerImage} ."
                    sh "docker tag ${dockerImage} rushigunjal1108/${dockerImage}"
                }
            }
        }

        stage('Push Docker Image to Registry') {
            steps {
                script {
                    def version = sh(script: 'echo $BUILD_NUMBER', returnStdout: true).trim()
                    def dockerImage = djangoapp:${version}"

                    // Push the Docker image to a registry (replace myregistry with your registry URL)
                    sh "docker push rushigunjal1108/${dockerImage}"
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    def version = sh(script: 'echo $BUILD_NUMBER', returnStdout: true).trim()
                    def dockerImage = "djangoapp:${version}"

                    // Deploy to Kubernetes using kubectl
                    sh "kubectl apply -f k8s-deployment.yaml --record=true --set=image=${dockerImage}"
                }
            }
        }
    }
}

