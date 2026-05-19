pipeline {
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
