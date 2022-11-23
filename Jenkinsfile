pipeline{

    agent any
       environment {
        PATH = "$PATH:/usr/share/maven"
    }
    stages{
        stage('Sonar Quality check'){
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