node{

   def mavenHome = tool name: 'maven3.9.3'
   
   echo "Node Name is: ${env.NODE_NAME}"
   echo "Build number is: ${env.BUILD_NUMBER}"
  
stage('CheckoutCode'){
git branch: 'development', credentialsId: '12ce556f-5d0a-4e2b-985d-059f88e9e3af', url: 'https://github.com/DadiSravs/Maven-web-application.git'
}

stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}
stage('ExecuteSonarubeReport'){
sh "${mavenHome}/bin/mvn clean sonar:sonar"
}
stage('UploadArtifacttoNexus'){
sh "${mavenHome}/bin/mvn clean deploy"
}
stage('DeployApplicationtoTomcat'){
    sshagent(['75dd4f3e-d053-4166-b908-07efb4cdfa4e']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.92.45:/opt/apache-tomcat-9.0.76/webapps/"
    }
}

}
