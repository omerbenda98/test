pipeline {
    agent any
    
    environment {
        GITHUB_CREDENTIALS = credentials('github-credentials')
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo "Starting checkout..."
                checkout scm
            }
        }
        
        stage('Print Info') {
            steps {
                sh '''
                    echo "Current directory:"
                    pwd
                    echo "\nRepository contents:"
                    ls -la
                    echo "\nGit status:"
                    git status
                '''
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline finished'
        }
        success {
            echo 'Pipeline succeeded'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}