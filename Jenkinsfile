pipeline{
  agent any
  stages{
    stage('Build'){
      tools {
        maven 'localMaven'
        jdk 'localJDK'
       }
      steps{
        bat 'C:/Users/balu/Documents/study/apache-maven-3.5.4/bin/mvn clean package'
      }
      post{
        success{
          echo 'Now Archiving .....'
          archiveArtifacts artifacts: '**/*.war'
        }
      }
      stage ('Deploy to staging'){
        build job: 'deploy-staging'
      }
    }
  }
}
