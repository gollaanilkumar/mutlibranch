
pipeline{
  tools{
    maven 'maven3'
  }
agent any
  stages{
   
   stage("BuilD"){
        steps{
          sh 'mvn clean package'
          sh 'mv target/myweb*.war target/multi.war'
        }
      }
    stage("docker build"){
      steps{
        sh "docker build . -t gollaanilkumar/docker:${getcommitId} "
      }
    }
    stage("docker push"){
      steps{
        withCredentials([string(credentialsId: 'dockerpass', variable: ''), string(credentialsId: 'dockerpass', variable: 'docker-pwd')]) {
        sh "docker login -u gollaanilkumar -p ${docker-pwd} "
        sh "docker push gollaanilkumar/docker:${getcommitId}"
      }
    }
    stage("docker dev deploy")
    {
      steps{
        
    sshagent(['docker']) {
      sh 'ssh -o StrictHostKeyCHecking=no ec2-user@172.31.34.47 docker rm -f dockerapp'
      sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.34.47 docker run -p 8090:8080 -d  --name dockerapp gollaanilkumar/docker:1'
    // some block
}
      }
    }
  }     
}
  
  def getcommitId(){
   commitid = sh returnStdout: true, script: 'git rev-parse --short HEAD'
   return commitid
  }
  
