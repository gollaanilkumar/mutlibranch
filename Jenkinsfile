
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
        sh 'docker build -t 65.2.3.63:8083/mywebapp:23 .'
      }
      }
    stage("docker push"){
      steps{
        sh 'docker login -u admin -p 1993Modi 65.2.3.63:8083'
        sh 'docker push 65.2.3.63:8083/mywebapp:23'
      } 
      
}
  }
}
