pipeline {
    agent any

        stage('Checkout') {
            echo 'Getting source code...'
            checkout scm
        }
        stage('Build') {
                echo 'Building'
		sh 'npm install'
        }
        stage('Start') {
                echo 'Running the app ..'
		sh 'pm2 start app.js'
        }
        stage('Test') {
                echo 'Testing the app ..'
		sh 'mocha'
	}
        stage('Stop') {
                echo 'Stoping the app ..'
                sh 'pm2 stop app.js'
        }
}

