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
        steps {
          echo 'Serverless profile create successfully'
        }
      }

      stage('Deploy' ) {
        steps {
           echo 'deploy successfully'
           sh 'sls deploy'
          } 
        }
    }

// Post statement used for notify the pipe line 
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
