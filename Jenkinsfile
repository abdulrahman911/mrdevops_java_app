@Library('my-shared-library') _

pipeline{
  agent any

  parameters{
    choice(name: 'action', choices: 'create\ndelete', description: 'Choose Create/Destroy ')
    string(name: 'DockerHubUser', description: "name of the dockerHub account", defaultValue: 'rahman777')
    string(name: 'ProjectName', description: "name of the project", defaultValue: 'javapp')
    string(name: 'ImageTag', description: "Image Tag", defaultValue: 'v1')
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

        // stage('Unit Test Maven'){
        // when { expression { params.action == 'create'} }    
        //     steps{
        //         script{
        //             mvnTest()
        //         }
        //     }
        // }

        // stage('Integration Test maven'){
        // when { expression { params.action == 'create'} }  
        //     steps{
        //         script{
        //             mvnIntegrationTest()
        //         }
        //     }
        // }

        // stage('Static Code Analysis: Sonarqube '){
        //     when { expression { params.action == 'create' } }
        //     steps{
        //        script {
        //             def SonarqubeCredentialsId = 'sonarqube-api'
        //             staticCodeAnalysis(SonarqubeCredentialsId)
        //        }
                
        //     }
        // }

        // stage('Quality Gate Status Check: Sonarqube'){
        //     when { expression { params.action == 'create'} }
        //     steps{
        //         script {

        //             def SonarqubeCredentials = 'sonarqube-api'
        //             qualityGateStatus(SonarqubeCredentials)
        //         }
        //     }
        // }

        stage('Maven Build'){
            when { expression { params.action == 'create' } }
            steps{
                script{
                    mvnBuild()
                }

            }
        }

        stage("Docker Image Build"){
            when { expression { params.action == 'create'} }
            steps{
                script{

                    dockerBuild("${params.DockerHubUser}", "${params.ProjectName}", "${params.ImageTag}")
                }
            }
        }
        stage("Docker Image Scan: Trivy"){
            when { expression { params.action == 'create'} }
            steps{
                script{

                    dockerImageScan("${params.DockerHubUser}", "${params.ProjectName}", "${params.ImageTag}")
                }
            }
        }   
        stage("Docker Image Push: DockerHub"){
            when { expression { params.action == 'create'} }
            steps{
                script{

                    dockerImagePush("${params.DockerHubUser}", "${params.ProjectName}", "${params.ImageTag}")
                }
            }
        } 
        stage("Docker Image Clean: JenkinHost"){
            when { expression { params.action == 'create'} }
            steps{
                script{

                    dockerImageCleanup("${params.DockerHubUser}", "${params.ProjectName}", "${params.ImageTag}")
                }
            }
        }        

    }
}