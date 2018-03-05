pipeline {
    agent any
    parameters{
    string(name: 'BRANCH_NAME', defaultValue: 'master', description: 'Branch to checkout' )
   }
      stages{
        stage('Checkout') {
	  steps {
            checkout([$class: 'GitSCM', branches: [[name: "$params.BRANCH_NAME"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/sagnikundu/pipeline-test.git']]])
	    dir ('tarball') {
                   writeFile file:'dummy', text:'dummy file'
                }
	  }
        }
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
        stage('****Test****') {
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
                sh "tar -zcvf tarball/'myapp_${env.BUILD_NUMBER}.tar.gz' .  --exclude='node_modules' --exclude='*.git*'"
                archiveArtifacts artifacts: 'tarball/*.tar.gz', fingerprint: true ,
                onlyIfSuccessful: true
      }
      failure {
		echo 'Failed to create artifacts ...'
      }
    }
}

