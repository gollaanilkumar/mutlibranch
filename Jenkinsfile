
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
        sh 'docker build -t 52.66.164.186:8083/mywebapp:24 .'
      }
      }
    stage("docker push"){
      steps{
        sh 'docker login -u admin -p 1993Modi 52.66.164.186:8083'
        sh 'docker push 52.66.164.186:8083/mywebapp:24'
      } 
      
}
    stage("docker deploy"){
      steps{
        sshagent(['docker-nexus']) {
     sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.47.141 sudo docker login -u admin -p 1993Modi 52.66.164.186:8083'
     sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.47.141 sudo docker pull 52.66.164.186:8083/mywebapp:24'
     sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.47.141 sudo docker run -p 8080:8080 -d --name nexusapp3 52.66.164.186:8083/mywebapp:24'
          
}
  }
}
  }
}
