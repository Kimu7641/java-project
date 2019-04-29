node('linux') {
  stage('Build') {
    git 'https://github.com/Kimu7641/java-project.git'
    sh "ant -f build.xml -v"
  }
  stage('Unit Tests') {
    sh "ant -f test.xml -v "
    junit "reports/result.xml"
    }
}
