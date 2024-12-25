pipeline {
    agent any
    
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
    }
    
    post {
        success {
            echo 'Git checkout successful!'
        }
        failure {
            echo 'Git checkout failed!'
        }
    }
}