pipeline {
    agent any

    environment {
        REGION = 'ap-south-1'
        IMAGE_TAG = "${BUILD_NUMBER}"
        AWS_ACCOUNT_ID = '439110395780'

        // DockerHub details
        DOCKERHUB_REPO = 'avikbhattacharya056/my-calculator-image'
        DOCKER_IMAGE = "${DOCKERHUB_REPO}:${IMAGE_TAG}"
        DOCKER_CREDENTIALS_ID = 'docker-hub-creds'

        // GitHub details
        GITHUB_REPO = 'https://github.com/AvikBhattacharya-Secops/Deploy-any-application-k8s-cluster-using-Jenkins-CI-CD-.git'
        GIT_CREDENTIALS_ID = 'GitAccess'

        // K8s (ArgoCD or Kubeconfig based) deployment
        KUBECONFIG_CREDENTIALS_ID = 'argocd'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: "${GIT_CREDENTIALS_ID}", url: "${GITHUB_REPO}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Push Docker Image to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        docker.image("${DOCKER_IMAGE}").push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                withCredentials([file(credentialsId: "${KUBECONFIG_CREDENTIALS_ID}", variable: 'KUBECONFIG')]) {
                    sh '''
                        echo "Using kubeconfig at $KUBECONFIG"

                        # Replace image tag dynamically in k8s-deployment.yaml
                        sed -i "s|image: .*|image: avikbhattacharya056/my-calculator-image:${BUILD_NUMBER}|" k8s-deployment.yaml

                        # Apply deployment
                        kubectl --kubeconfig=$KUBECONFIG apply -f k8s-deployment.yaml
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline completed successfully. Image pushed: ${DOCKER_IMAGE}"
        }
        failure {
            echo "❌ Pipeline failed."
        }
    }
}
