pipeline{

    agent any

    stages{

        stage('Sonar Quality check'){

              agent {

                docker {

                    image 'maven'
                }

              }
            steps{

                script{
                    withSonarQubeEnv(credentialsId: 'sonarqube-token') {
                    sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
    }
}