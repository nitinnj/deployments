pipeline {
    agent any

    stages {

        stage('Pull Latest Code') {
            steps {
                sh '''
                cd ~/projects/admin && git pull
                cd ~/projects/backend && git pull
                cd ~/projects/web && git pull
                cd ~/projects/strapi && git pull
                cd ~/projects/deployments && git pull
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                cd ~/projects/deployments
                docker compose up -d --build
                '''
            }
        }

    }
}
