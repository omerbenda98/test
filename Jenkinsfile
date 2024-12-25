pipeline {
    agent any
    
    tools {
        nodejs 'nodejs'
    }
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        GITHUB_CREDENTIALS = credentials('github-credentials')
        DOCKER_IMAGE = 'omerbenda98/puppy-adoption-frontend'
        BRANCH_NAME = "${params.BRANCH_NAME ?: 'staging'}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo "Starting checkout..."
                checkout scm
            }
        }
        
        stage('Git Info') {
            steps {
                sh '''
                    echo "Git Status:"
                    git status
                    echo "\nCurrent Branch:"
                    git branch
                    echo "\nRemote Info:"
                    git remote -v
                '''
            }
        }

        stage('Docker Build Simulation') {
            steps {
                echo "Would execute these Docker commands:"
                echo "docker login with provided credentials"
                echo "docker build -t ${DOCKER_IMAGE}:v1.${BUILD_NUMBER}"
                echo "docker push ${DOCKER_IMAGE}:v1.${BUILD_NUMBER}"
            }
        }

        stage('Update K8s Manifests Simulation') {
            steps {
                script {
                    def targetPath = BRANCH_NAME == 'main' ? 'main' : 'staging'
                    def targetNamespace = BRANCH_NAME == 'main' ? 'production' : 'staging'
                    
                    echo """
                        Would execute these K8s update commands:
                        1. Remove k8s-repo if exists
                        2. Configure git user
                        3. Clone k8s repo
                        4. Update deployment.yaml with new image: ${DOCKER_IMAGE}:v1.${BUILD_NUMBER}
                        5. Commit and push changes to ${targetPath}/frontend/deployment.yaml
                    """
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline successful!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}