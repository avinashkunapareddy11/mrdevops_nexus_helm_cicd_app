pipeline {
    agent any 
        stages {
            stage('sonar quality check') {
            agent {
                docker {
                    image 'maven:3.9.0-eclipse-temurin-11'
                    args '-v /root/.m2:/root/.m2'

            
                }
            }
            steps {
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-Token') {
                    sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }

            stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
    }
}
