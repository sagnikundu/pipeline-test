pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building'
		sh 'npm install'
            }
        }
        stage('Start') {
            steps {
                echo 'Running the app ..'
		sh 'pm2 start app.js'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the app ..'
		sh 'mocha'
            }
        stage('Stop') {
            steps {
                echo 'Stoping the app ..'
                sh 'pm2 stop app.js'
            }
        }
    }
}
