pipeline {
    agent any

    environment {
        PROJECT_DIR = "/home/ubuntu/projects"
    }

    stages {

        stage('Verify Environment') {
            steps {
                sh '''
                    whoami
                    docker --version
                    docker compose version
                '''
            }
        }

        stage('Pull Latest Code') {
            steps {
                sh '''
                    cd $PROJECT_DIR/admin && git pull origin main
                    cd $PROJECT_DIR/backend && git pull origin main
                    cd $PROJECT_DIR/web && git pull origin main
                    cd $PROJECT_DIR/strapi && git pull origin main
                    cd $PROJECT_DIR/deployments && git pull origin main
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    cd $PROJECT_DIR/deployments
                    docker compose up -d --build
                '''
            }
        }

        stage('Verify Containers') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful 🚀'
        }

        failure {
            echo 'Deployment failed ❌'
        }
    }
}
