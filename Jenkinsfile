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

        stage('Unit Test Maven'){
            steps{
                script{
                    mvnTest()
                }
            }
        }

        stage('Integration Test maven'){
            steps{
                script{
                    mvnIntegrationTest()
                }
            }
        }

    }


}