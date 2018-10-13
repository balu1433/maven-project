pipeline{
  agent any
  stages{
    stage('Init'){
      steps{
        bat 'set M2_HOME=C:\Users\balu\Documents\study\apache-maven-3.5.4'
        bat 'set path=%path%%M2_HOME%/bin'
      }
    stage('Build'){
      steps{
        bat 'mvn clean package'
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
