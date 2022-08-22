pipeline {
environment {
    BRANCH_NAME = "${env.BRANCH_NAME}"
}
agent any
stages{
    stage('QA') {
        steps{
        withCredentials([[
            $class: 'AmazonWebServicesCredentialsBinding', 
            accessKeyVariable: 'AWS_ACCESS_KEY_ID', 
            credentialsId: 'Jenkins_ID', 
            secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh "aws s3 ls"
            sh "aws s3 cp index.html s3://demo-app-54321/index.html"
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
        withCredentials([[
            $class: 'AmazonWebServicesCredentialsBinding', 
            accessKeyVariable: 'AWS_ACCESS_KEY_ID', 
            credentialsId: 'Jenkins_ID', 
            secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh "aws s3 ls"
            sh "aws s3 cp index.html s3://proddemoapplication/index.html"
         }     
               
                 
                 
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
}
}
/*stage('artifacts to s3') {
      steps {
      withCredentials([[
          $class: 'AmazonWebServicesCredentialsBinding', 
          accessKeyVariable: 'AWS_ACCESS_KEY_ID', 
          credentialsId: 'Jenkins_ID', 
          secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
         sh "aws s3 ls"
         sh "aws s3 cp index.html s3://demo-app-54321/index.html"
         sh "aws s3 cp index.html s3://proddemoapplication/index.html"
      }
          
      }
   } 
