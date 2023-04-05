@Library('my-shared-library') _

pipeline{
  agent any

    stages{   
        
        stage('Git checkout'){
        steps{
                gitCheckout(
                branch: "main",
                url: "https://github.com/abdulrahman911/mrdevops_java_app.git"
              )            
        }
    }
    }


}