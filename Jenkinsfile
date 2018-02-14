
node('maven') {
 	// clean workspace
    deleteDir()
 
    
        stage ('Clone') {
        	checkout scm
        }



          stages {
              stage('Build') {
                  steps {
                      sh 'mvn -B package'
                  }
              }
          }
}
