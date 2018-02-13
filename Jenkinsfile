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
// Convenience Functions to read variables from the pom.xml
def getVersionFromPom(pom) {
  def matcher = readFile(pom) =~ '<version>(.+)</version>'
  matcher ? matcher[0][1] : null
}
def getGroupIdFromPom(pom) {
  def matcher = readFile(pom) =~ '<groupId>(.+)</groupId>'
  matcher ? matcher[0][1] : null
}
def getArtifactIdFromPom(pom) {
  def matcher = readFile(pom) =~ '<artifactId>(.+)</artifactId>'
  matcher ? matcher[0][1] : null
}
