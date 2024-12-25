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