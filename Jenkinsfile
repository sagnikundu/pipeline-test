pipeline {
    agent none

      stages{
        stage('Build') {
	  steps {
                echo 'Building'
                sh 'ls -ltr'
		sh 'npm install'
	  }
        }
        stage('Start') {
	  steps {
                echo 'Running the app ..'
		sh 'pm2 start app.js'
	  }
        }
        //stage('Test') {
	 // steps {
          //      echo 'Testing the app ..'
	//	sh 'mocha'
	 // }
	//}
        stage('***Stop') {
	  steps {
                echo 'Stoping the app ..'
                sh 'pm2 stop app.js'
	  }
        }
    }
    //post {
      //success {
        //        sh "tar -zcvf tarball/'myapp_${env.BUILD_NUMBER}.tar.gz' .  --exclude='node_modules' --exclude='*.git*'"
        //        archiveArtifacts artifacts: 'tarball/*.tar.gz', fingerprint: true ,
       //         onlyIfSuccessful: true
     // }
     // failure {
	//	echo 'Failed to create artifacts ...'
      //}
   // }
}

