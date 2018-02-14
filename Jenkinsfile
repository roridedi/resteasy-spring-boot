
node('maven') {
 	// clean workspace
    deleteDir()
 
    
  



          stages {
           
                 stage ('Clone') {
        	checkout scm
        }
              stage('Build') {
                  steps {
                      sh 'mvn -B package'
                  }
              }
          }
}
