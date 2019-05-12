node('linux') {
  stage('Build') {
    git 'https://github.com/Kimu7641/java-project.git'
    sh "ant -f build.xml -v"
  }
  stage('Unit Tests') {
    sh "ant -f test.xml -v "
    junit "reports/result.xml"
  }
  stage('Deploy') {
    sh "aws s3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://bucket-for-jenkins"
  }
  stage('Report') {
    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'e454ad3b-9be1-4522-90c2-673291a9ee20', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
      sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins" 
    }
  }
}
