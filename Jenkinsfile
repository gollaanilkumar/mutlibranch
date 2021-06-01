
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
        sh 'docker build -t gollaanilkumar/docker:1 .'
      }
    }
    stage("docker push"){
      steps{
        sh 'docker login -u gollaanilkumar -p 1993Modi'
        sh 'docker push gollaanilkumar/docker:1'
      }
    }
  }     
}
