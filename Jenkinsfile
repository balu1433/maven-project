pipeline{
  agent any
  stages{
    stage('Build'){
      steps{
        bat 'C:/Users/balu/Documents/study/apache-maven-3.5.4/bin/mvn clean package'
      }
      post{
        success{
          echo 'Now Archiving .....'
          archiveArtifacts artifacts: '**/*.war'
        }
      }
    }
  }
}
