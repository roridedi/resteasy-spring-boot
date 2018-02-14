
node('groovy') {
 	// clean workspace
    deleteDir()
agent any
  tools {
    maven 'M3'
  }
    try {
        stage ('Clone') {
        	checkout scm
        }
        stage ('Build') {
        	sh "echo 'shell scripts to build project...'"
          sh 'mvn clean install'
        }
        stage ('Tests') {
	        parallel 'static': {
	            sh "echo 'shell scripts to run static tests...'"
	        },
	        'unit': {
	            sh "echo 'shell scripts to run unit tests...'"
	        },
	        'integration': {
	            sh "echo 'shell scripts to run integration tests...'"
	        }
        }
      	stage ('Deploy') {
            sh "echo 'shell scripts to deploy to server...'"
      	}
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
