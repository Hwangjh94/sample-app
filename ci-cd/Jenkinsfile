pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "hwangjh94/sample-app"
        DOCKER_TAG = "latest"
        KUBE_CONFIG = credentials('kubeconfig')  // 젠킨스에 Kubeconfig 저장 후 사용
    }

    stages {
        stage('Checkout Source') {
            steps {
                git branch: 'main', credentialsId: 'github-credentials', url: 'https://github.com/Hwangjh94/sample-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $DOCKER_IMAGE:$DOCKER_TAG ."
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                        sh "docker push $DOCKER_IMAGE:$DOCKER_TAG"
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    withKubeConfig([credentialsId: 'kubeconfig']) {
                        sh "kubectl apply -f k8s/manifests/deployment.yaml"
                        sh "kubectl apply -f k8s/manifests/service.yaml"
                        sh "kubectl apply -f k8s/manifests/ingress.yaml"
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Deployment completed successfully!"
        }
        failure {
            echo "Build or deployment failed!"
        }
    }
}
