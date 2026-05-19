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

        stage('Docker Build & Deploy') {
            steps {
                sh '''
                cd $PROJECT_DIR/deployments

                docker compose up -d --build
                '''
            }
        }

        stage('Cleanup Unused Docker Resources') {
            steps {
                sh '''
                docker image prune -af
                '''
            }
        }

        stage('Verify Running Containers') {
            steps {
                sh '''
                docker ps
                '''
            }
        }
    }

    post {

        success {
            echo 'Application deployed successfully 🚀'
        }

        failure {
            echo 'Deployment failed ❌'
        }
    }
}pipeline {
    agent any

    stages {

        stage('Pull Latest Code') {
            steps {
                sh '''
                cd /home/ubuntu/projects/admin && git pull
                cd /home/ubuntu/projects/backend && git pull
                cd /home/ubuntu/projects/web && git pull
                cd /home/ubuntu/projects/strapi && git pull
                cd /home/ubuntu/projects/deployments && git pull
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                cd /home/ubuntu/projects/deployments
                docker compose up -d --build
                '''
            }
        }

    }
}
