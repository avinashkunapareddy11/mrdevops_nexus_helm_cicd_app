pipeline {
    agent any 
        stages {
            stage('sonar quality check') {
            agent {
                docker {
                    image 'maven:latest'
                }
            }
            steps {
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                    sh 'mvn clean pacakge sonar:sonar'
                    }
                }
            }
        }
    }
}