pipeline {
  agent any
  tools {nodejs "node"}

  parameters {
      password(name: 'SERVERLESS_ACCESS_KEY', defaultValue: 'SECRET', description: 'Enter a password')
    }
  stages {
      
    stage('build' ) {

      steps {
         //sh 'npm install'
         echo "Build Number: ${env.BUILD_NUMBER}"
          echo "Hello ${params.SERVERLESS_ACCESS_KEY}"

          //echo "SERVERLESS_ACCESS_KEY is ${SERVERLESS_ACCESS_KEY}"
       // echo "SECRET is ${SECRET}"

        } 
      }

    stage('Test' ) {
      // Test cases only execute when branch name should dev
      when {
        expression {
          // BRANCH_NAME is env variable in jenkins
          env.BRANCH_NAME == 'dev'
        }
      }

      steps {
         echo 'Testing the application'
        } 
      }

      stage('Config'){
        environment {
            //SERVICE_CREDS = credentials('my-predefined-username-password')
            SERVICE_CREDS=credentials('aws-creds')

        }
        
        steps {
          sh "echo Service user is ${SERVICE_CREDS_USR}"

          //sh "serverless config credentials --provider aws --key ${SERVERLESS_ACCESS_KEY} --secret ${SECRET} --profile serverlessUserProfile -o"
          echo 'Serverless profile create successfully'
        }
      }

      stage('Deploy' ) {
        steps {
           sh 'sls deploy'
           echo 'deploy successfully'
          } 
        }
    }

// Post statement used for notify the pipe lines
    // post {
    //   always {
    //    // execute every time when pipe line
    //    echo 'always execute'
    //   }
    //   failure {
    //    // excute this statment when pipe line failed
    //    echo 'failure case execute'
    //   }
    //   success {
    //     // execute this statement when pipe line was successed
    //     echo 'success execute'
    //   }
    // }
}
