pipeline {
    agent {
        docker {
            image 'node:6-alpine' 
            args '-p 3000:3000' 
        }
    }
    environment {
    	CI = 'true'
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm config set proxy http://UC00001:F8416987@194.114.63.23:8080; npm config set https-proxy http://UC00001:F8416987@194.114.63.23:8080; npm install' 
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
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
