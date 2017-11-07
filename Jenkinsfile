pipeline {
    agent any
      stages{
        stage('Checkout') {
	  steps {
            checkout scm
	    dir ('tarball') {
                   //writeFile file:'dummy', text:''
                }
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
                sh "tar -zcvf 'myapp_${env.BUILD_NUMBER}.tar.gz' tarball/  --exclude='*.git*'"
                archiveArtifacts artifacts: '*.tar.gz', fingerprint: true ,
                onlyIfSuccessful: true
      }
      failure {
		echo 'Failed to create artifacts ...'
      }
    }
}

