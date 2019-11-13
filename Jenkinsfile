pipeline {
    agent { node { label 'slave_new' } }
    
        
        stages { 

    stage('Checkout') { 

      steps { 

        checkout([ 

          $class: 'GitSCM', 

          branches: [[name: '*/qa']], 

          userRemoteConfigs: [[credentialsId: '901eea44-a582-448f-997d-7016c48363e5', 

          url: 'https://github.com/busani9/Jenkins.Dotnet.Core.Ubuntu.git']] 

        ]) 

      } 

    } 
      
            stage('build') {
                steps { 
sh 'sudo systemctl stop test.service'
sh 'sudo systemctl stop nginx'
sh 'sudo dotnet publish --configuration release'
sh 'sudo systemctl start test.service'
sh 'sudo systemctl start nginx'
                   
                }
            }
            
    
    }
    post {  
 success { 
        mail to: 'amarender.busani9@gmail.com',
          subject: "Job Success:  '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          body: "Check console output at '${env.BUILD_URL}' for furthur details"    
              }    
               failure { 
        mail to: 'amarender.busani9@gmail.com',
          subject: "Job Failed:  '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          body: "Check console output at '${env.BUILD_URL}' for furthur details" 
              } 
    }
    
    }
    
