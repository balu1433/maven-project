pipeline{
  agent any
  paramerters{
      string(name: 'tomcat_dev', defaultValue: '13.57.28.133', description: 'staging server')
      string(name: 'tomcat_prod', defaultValue: '54.183.138.36', description: 'production server')
    
  }
  triggers{
    pollSCM(' * * * * *')
  }
  stages{
    stage('Build'){
        tools{
          maven 'localMaven'
          jdk 'localJDK'
        }
        steps{
          bat 'mvn clean package'
        }
        post {
          success {
            echo 'NOW ARCHIVING'
            archiveArtifacts artifacts: '**/*.war'
          }
        }
    stage('Deployment'){
      parellel{
        stage('Deploy to staging'){
          steps{
            bat "winscp -i C:\Users\balu\Documents\study\aws\tomcat-demo.pem **\target\*.war ec2-user@${paramerters.tomcat_dev}:/var/lib/tomcat/webapps"
          }
        }
        stage('Deploy to Prod'){
          steps{
              bat "winscp -i C:\Users\balu\Documents\study\aws\tomcat-demo.pem **\target\*.war ec2-user@${paramerters.tomcat_prod}:/var/lib/tomcat/webapps"
          }
        }
      }
    }    
  }
 }
}

