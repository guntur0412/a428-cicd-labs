pipeline {
    agent {
        docker {
            image 'node:lts-bullseye-slim'
            args '-p 30000:30000'
        }
    }

    options {
        skipDefaultCheckout()
    }

    stages {
        stage('Start') {
            steps {
                echo 'Memulai Proses Pipeline'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Proses Build Dimulai...'
                sh 'npm install'
                sh 'export NODE_OPTIONS=--openssl-legacy-provider && npm run build'
            }
        }

        stage('Test') {
            steps {
                echo 'Menjalankan Test...'
                sh 'CI=true npm test -- --watchAll=false'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Melakukan Deploy aplikasi (simulasi)...'
                sh './jenkins/scripts/deliver.sh'
            }
        }

        stage('End') {
            steps {
                echo 'Pipeline Selesai ✅'
            }
        }
    }
}
