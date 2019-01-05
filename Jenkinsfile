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
   } 
}
