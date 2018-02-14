
node('jenkins-slave-maven-rhel7') {
 	// clean workspace
    deleteDir()
    tools {
        maven 'M3'
    }
    
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
