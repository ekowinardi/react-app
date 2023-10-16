pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim'
            args '-p 3000:3000'
            args '-u 0:0'
        }
    }
    environment {
	        PUBLIC_URL = 'dbs-react.web.app/'
	    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approval') {
            steps {
                input message: 'Lanjut ke tahap deploy?'
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                sleep(time: 1, unit: 'MINUTES')
                sh './jenkins/scripts/kill.sh' 
                sh './jenkins/scripts/deploy-to-firebase.sh'
            }
        }
    }
}