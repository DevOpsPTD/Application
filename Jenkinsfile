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


}
     
