pipeline{
agent any

tools{
maven 'maven-3.8.4'
}

stages{
  stage('GIT CheckOutCode'){
    steps{
    git credentialsId: '12035451-f4d9-4f48-842a-cc591636fe83', url: 'https://github.com/Manoj-0218/maven-web-application.git'
   }
  }
stage('Build'){
  steps{
    sh "mvn clean package"
   }	
  }
  
stage('SonarQube Report'){
  steps{
    sh "mvn clean sonar:sonar"
   }	
  }
stage ('UploadArtifactsIntoNexus'){
  steps{
    sh "mvn clean deploy"
   }
  }
  
stage('DeployToTomcat'){
    steps{
    sshagent(['12035451-f4d9-4f48-842a-cc591636fe83']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.111.197.60:/opt/apache-tomcat-9.0.58/webapps/"
}
}
}
 
}
}
