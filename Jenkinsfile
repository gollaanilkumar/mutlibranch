
pipeline{
agent any
  tools{
    maven 'maven3' 
  }
  stages{
    stage("SCM BUILD"){
      when {
        branch "develop"
      }
      steps{
        git branch: 'develop', url: 'https://github.com/gollaanilkumar/mutlibranch'
      }
    }
      stage(" maven BuilD"){
        steps{
          sh 'mvn clean package'
          sh 'mv target/myweb*.war target/multi.war'
        }
      }
      stage("Nexus uplaod"){
        when {
        branch "develop"
      }
        steps{
          nexusArtifactUploader artifacts: [[artifactId: 'myweb', classifier: '', file: 'target/multi.war', type: 'war']],
          credentialsId: 'nexus3',
           groupId: 'in.javahome', 
            nexusUrl: '172.31.6.193:8081', 
            nexusVersion: 'nexus3',
            protocol: 'http', 
            repository: 'javahome-release',
            version: '0.0.2'
        }
      }
    stage("Deploy to uat")
    {
      when {
        branch "develop"
      }
      steps{
        sshPublisher(publishers: [sshPublisherDesc(configName: 'tomcat', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '/opt/tomcat8/bin/startup.sh', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'mywebdev*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
          
}
      }
    }
    
        stage("Deploy to prod")
    {
      when {
        branch "master"
      }
      steps{
        echo "prod deploy"
      }
    }
    
  }
}
    


