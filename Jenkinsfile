
node {
 	// clean workspace
    deleteDir()
    tools {
        maven 'M3'
    }
    try {
        stage ('Clone') {
        	checkout scm
        }
        
      

          stages {
              stage('Build') {
                  steps {
                      sh 'mvn -B package'
                  }
              }
          }(err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
