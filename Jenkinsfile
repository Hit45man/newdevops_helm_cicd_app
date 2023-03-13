pipeline {
    
    agent any
    
    tools {
        
       maven 'Maven3'
       
     }
       stages {
        
           stage('Git Checkout'){
            
              steps {
                
                git branch: 'main', url: 'https://github.com/Hit45man/newdevops_helm_cicd_app.git'
                
            }
            
        }
        stage('Unit testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                    
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
            stage('Maven build'){
            
                steps{
                
                   script{
                    
                      sh 'mvn clean install'
               
            }
        }
    }
        stage('Static Code Analysis'){
            
            steps{
                
                script{
                    
                   withSonarQubeEnv(credentialsId: 'sonar-auth-jenkins'){
                   
                    sh 'mvn clean package sonar:sonar'
                       
                   }
                        
                }
                
            }
        }
        stage('Build Docker image'){
            steps{
                script{
                        sh 'cd /var/lib/jenkins/workspace/Demo-pipeline'
                        sh 'docker image  build -t $JOB_NAME:v.1.$BUILD_ID .'
            }
        }
     }
        stage('Tag the docker image'){
            steps{
                script{
                    sh 'cd /var/lib/jenkins/workspace/Demo-pipeline'
                    sh 'docker image tag $JOB_NAME:v.1.$BUILD_ID rohikam/$JOB_NAME:v.1.$BUILD_ID'
                    sh 'docker image tag $JOB_NAME:v.1.$BUILD_ID rohikam/$JOB_NAME:latest'
                }
            }
        }
        stage('Push Image to Docker Hub'){
            steps{
                script{
                    withCredentials([usernamePassword(credentialsId: 'docker_login', passwordVariable: 'docker_pass', usernameVariable: 'docker_user')]) {
                        
                     sh "docker login -u ${docker_user} -p ${docker_pass}"
                     
                     sh 'cd /var/lib/jenkins/workspace/Demo-pipeline'
                     
                     sh 'docker image push  rohikam/$JOB_NAME:v.1.$BUILD_ID'
                     
                     sh 'docker image push  rohikam/$JOB_NAME:latest'
                     
                     sh 'docker image rm  rohikam/$JOB_NAME:v.1.$BUILD_ID  rohikam/$JOB_NAME:latest'
                   }
                }
            }
        }
   }
}