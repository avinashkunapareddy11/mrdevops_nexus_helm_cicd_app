pipeline {
    agent any 
        stages {
            stage('sonar quality check') {
            agent {
                docker {
                    image 'maven'
                    args '-v /root/.m2:/root/.m2'

            
                }
            }
            steps {
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                    sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
    }
}
