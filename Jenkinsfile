node {
 	// clean workspace
    deleteDir()

    try {
        stage ('Clone') {
        	checkout scm
        }
        stage ('Build') {
        	sh "echo 'shell scripts to build project...'"
        }
        stage('Build war') {
          echo "Building version"

          sh "${mvnCmd} clean package -DskipTests"
        }
        stage('Unit Tests') {
          echo "Unit Tests"
          sh "${mvnCmd} test"
        }
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
