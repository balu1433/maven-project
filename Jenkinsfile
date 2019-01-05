pipeline{
  agent any
  parameters{
      string(name: 'tomcat_dev', defaultValue: '13.57.28.133', description: 'staging server')
      string(name: 'tomcat_prod', defaultValue: '54.183.138.36', description: 'production server')
    
  }

     stage('Build'){
                  tools{
                      maven 'mvn'
                      jdk 'jdk'
                  }
                  steps{
                      sh 'mvn clean package'
                  }
                  post {
                      success {
                          echo 'NOW ARCHIVING'
                          archiveArtifacts artifacts: '**/*.war'
                      }
                  }
      }
      stage('Deployment'){
            parallel{
                  stage('Deploy to staging'){
                      steps{
                            sh "scp -i C:/Users/balu/Documents/study/aws/tomcat-demo.pem C:/Users/balu/.jenkins/workspace/PipelineAsCodeExample/webapp/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat/webapps"
                      }
                  }
                  stage('Deploy to Prod'){
                      steps{
                            sh "scp -i C:/Users/balu/Documents/study/aws/tomcat-demo.pem C:/Users/balu/.jenkins/workspace/PipelineAsCodeExample/webapp/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat/webapps"
                      }
                  }
            }
      }    
  }
}
