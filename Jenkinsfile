pipeline{
  agent any
  stages{
        stage('Build'){
                      tools {
                           maven 'localMaven'
                           jdk 'localJDK'
                      }
                      steps{
                           bat 'C:/Users/balu/Documents/study/apache-maven-3.5.4/bin/mvn clean package -Dbuild_number=BUILD_NUMBER'
                      }
                      post{
                          success{
                                echo 'Now Archiving .....'
                                archiveArtifacts artifacts: '**/*.war'
                          }
                      }
        }
        stage ('Deploy to staging'){
              steps{
                   build job: 'deploy-staging'
              }
        } 
        stage ('Deploy to Production'){
          steps{
            timeout(time:5, unit:'DAYS'){
                input message : 'Approve PRODUCTION Deployment'
                 }
                build job: 'deploy-prod'
          }
          post{
            success{
                echo "Production deployment is successful" 
            }
            failure{
                echo "Deployment Failed"
            }
          }
        }
  }
}
