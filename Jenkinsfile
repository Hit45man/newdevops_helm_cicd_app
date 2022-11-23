pipeline{

    agent any
       environment {
        PATH = "$PATH:/usr/share/maven"
    }
    stages{
        stage('Sonar Quality check'){
            steps{

                script{
                    withSonarQubeEnv('SonarQube') {
                    sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
    }
}