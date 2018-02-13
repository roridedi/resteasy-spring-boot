node('maven')  {
 	// clean workspace
    deleteDir()
  def groupId    = getGroupIdFromPom("pom.xml")
  def artifactId = getArtifactIdFromPom("pom.xml")
  def version    = getVersionFromPom("pom.xml")
    try {
        stage ('Clone') {
        	checkout scm
        }
   stage('Build war') {
    echo "Building version ${version}"

    sh "${mvnCmd} clean package -DskipTests"
  }
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
