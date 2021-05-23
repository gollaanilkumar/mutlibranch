
pipeline{
  tools{
    maven 'maven3'
  }
agent any
  stages{
    stage("SCM BUILD"){
      steps{
        git branch: 'master', url: 'https://github.com/gollaanilkumar/mutlibranch'
      }
    }
      stage("BuilD"){
        steps{
          sh 'mvn clean package'
          sh 'mv target/myweb*.war target/multi.war'
        }
      }
      stage("Nexus uplaod"){
        steps{
          script{
        def pom = readMavenPom file: 'pom.xml'
        def repository= pom.version
        if (repository.endsWith("SNAPSHOT")) {
           repository = 'javahome-snapshot'
        }
        else {
            repository = 'javahome-release'
        }
        
          nexusArtifactUploader artifacts: [[artifactId: 'myweb', classifier: '', file: 'target/multi.war', type: 'war']],
          credentialsId: 'nexus3',
           groupId: 'in.javahome', 
            nexusUrl: '172.31.6.193:8081',
            nexusVersion: 'nexus3',
            protocol: 'http', 
            repository: repository,
            version: pom.version
        }
      }
      }
  }     
}
