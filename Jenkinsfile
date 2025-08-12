pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim'
            args '-p 3000:3000'
            args '--network=host'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
		sh 'HOST=0.0.0.0 npm start &'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}


     stage('Deploy') {
    	agent any
    	steps {
        	sh '''
       		docker build -t react-app .
        	docker rm -f react-running || true
        	docker run -d --name react-running -p 3000:3000 react-app
        	'''
         }
     }

