pipeline {
    agent any
      stages{
        stage('Checkout') {
	  steps {
            echo 'Getting source code...'
            checkout scm
	  }
        }
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
	}
        stage('Stop') {
	  steps {
                echo 'Stoping the app ..'
                sh 'pm2 stop app.js'
	  }
        }
    }
    post {
      success {
		sh "sleep 5s"
                sh "tar -zcvf 'myapp_${env.BUILD_NUMBER}.tar.gz' ."
                archiveArtifacts artifacts: '*.tar.gz', fingerprint: true ,
                onlyIfSuccessful: true
      }
      failure {
		echo 'Failed to create artifacts ...'
      }
    }
}

