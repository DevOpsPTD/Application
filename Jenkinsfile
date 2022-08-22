pipeline {
environment {
    BRANCH_NAME = "${env.BRANCH_NAME}"
}
agent any
stages{
    stage('Build-Initiator-Info'){
            steps{
                sh 'echo "Send Info"'
            }
    }
    stage('QA') {
        steps{
             catchError {
                sh 'echo "This is QA-build"'
               
                 
                 
            }
         }
         post {
            success {
                echo 'Compile Stage Successful . . .'
            }
            failure {
                echo 'Compile stage failed'
                error('Stopping early…')

             }
    }
   }
  stage ('Deploy To Prod'){
  input{
    message "Do you want to proceed for production deployment?"
  }
      
      
    steps {
                sh 'echo "Deploy into Prod"'

              }
        }
  
  stage('PROD') {
        steps{
             catchError {
                sh 'echo "This is Prod-build"'
               
                 
                 
            }
         }
         post {
            success {
                echo 'Compile Stage Successful . . .'
            }
            failure {
                echo 'Compile stage failed'
                error('Stopping early…')

             }
    }
   }

  stage('artifacts to s3') {
      try {
      // you need cloudbees aws credentials
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'deploytos3', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
         sh "aws s3 ls"
         sh "aws s3 cp "index.html" "s3://demo-app-54321/index.html""
         sh "aws s3 cp "index.html" "s3://proddemoapplication/index.html""
      } catch(err) {
         sh "echo error in sending artifacts to s3"
      }
   }
  }

