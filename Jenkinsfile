
pipeline {
    agent any

    environment {
        BOT_TOKEN = '6812251935:AAFxjvNYIPzEn3G6JXfvkqy_C4hQi9T36gQ'
        CHAT_ID = '782285470'
    }

    stages {
        stage('Git Checkout') {
            steps {
                echo 'Code checkout.'
                git branch: 'final', url: 'https://github.com/SereyvicheaSaro/DevOps.git'
            }
        }
        stage('Build using Tools') {
            steps {
                echo 'Compiling code...'
                sh 'cp .env.example .env'
                sh 'composer install && php artisan key:generate && npm install && npm run build'
            }
        }
        stage('Test the app') {
            steps {
                echo 'Testing unit tests...'
                echo 'Testing features...'
                sh 'php artisan test'
            }
        }
    }

    post {
        success {
            sh '''
                bash scripts/deployment.sh SUCCESS🟢
            '''
        }
        failure {
            sh '''
                bash scripts/deployment.sh FAILED🔴
            '''
        }
    }
}