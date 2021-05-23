
pipeline{
  tools{
    maven 'maven3'
  }
agent any
  stages{
    stage("SCM BUILD"){
      steps{
        git branch: 'develop', url: 'https://github.com/gollaanilkumar/mutlibranch'
      }
    }
      stage("BuilD"){
        steps{
          sh 'mvn clean package'
          sh 'mv target/myweb*.war target/multi.war'
        }
      }
      stage("Nexus uplaod"){
        def pom = readMavenPom file: 'pom.xml'
        def repository= pom.repository
        if repository.endsWith("SNAPSHOT") {
           repository = 'javahome-snapshot'
        }
        else {
            repository = 'javahome-release'
        }
        
        
        steps{
          nexusArtifactUploader artifacts: [[artifactId: 'myweb', classifier: '', file: 'target/multi.war', type: 'war']],
          credentialsId: 'nexus3',
           groupId: 'in.javahome', 
            nexusUrl: '172.31.37.225:8081', 
            nexusVersion: 'nexus3',
            protocol: 'http', 
            repository: 'javahome-release',
            version: '0.0.1'
        }
      }
  }     
}
