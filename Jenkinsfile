pipeline{
  agent any
  parameters{
      string(name: 'tomcat_dev', defaultValue: '13.57.28.133', description: 'staging server')
      string(name: 'tomcat_prod', defaultValue: '54.183.138.36', description: 'production server')
    
  }
  
   stages{
      stage('Scm'){
        steps{
          checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/balu1433/maven-project.git']]])
        }
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
                            scp -i /var/tmp/tomcat-demo.pem webapp/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat/webapps"
                      }
                  }
                  stage('Deploy to Prod'){
                      steps{
                            scp -i /var/tmp/tomcat-demo.pem webapp/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat/webapps"
                      }
                  }
            }
      }    
  }
}
