@Library('my-shared-library') _

pipeline{
  agent any

  parameters{
    choice(name: 'action', choices: 'create\ndelete', description: 'Choose Create/Destroy ')
  }

    stages{   
        
        stage('Git checkout'){
        when { expression { params.action == 'create'} }
        steps{
                gitCheckout(
                branch: "main",
                url: "https://github.com/abdulrahman911/mrdevops_java_app.git"
              )            
            }
        }

        stage('Unit Test Maven'){
        when { expression { params.action == 'create'} }    
            steps{
                script{
                    mvnTest()
                }
            }
        }

        stage('Integration Test maven'){
        when { expression { params.action == 'create'} }  
            steps{
                script{
                    mvnIntegrationTest()
                }
            }
        }

        stage('Static Code Analysis: Sonarqube '){
            when { expression { params.action == 'create' } }
            steps{
               
                    def SonarqubeCredentialsId = 'sonarqube-api'
                    staticCodeAnalysis(SonarqubeCredentialsId)
                
            }
        }

        stage('Quality Gate Status Check: Sonarqube'){
            when { expression { params.action == 'create'} }
            steps{
                script {
                        
                    def SonarqubeCredentialsId = 'sonarqube-api'
                    qualityGateStatus(SonarqubeCredentialsId)
                }
            }
        }


    }


}