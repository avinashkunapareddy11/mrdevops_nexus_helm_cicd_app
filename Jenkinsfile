pipeline {
    agent any 
    environment {
        VERSION = "${env.BUILD_ID}"
    }
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

            stage('Quality Gate status') {
                steps {
                    script{
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-Token'
                    }
                }
            }
            stage('docker build & docker push to Nexus repo'){
                steps{
                    script{
                        withCredentials([string(credentialsId: 'nexus_passwd', variable: 'nexus_creds')]) {
                        sh '''
                        docker build -t 35.171.158.68:8083/springapp:${VERSION} .
                        docker login -u admin -p $nexus_creds 35.171.158.68:8083
                        docker push 35.171.158.68:8083/springapp:${VERSION}
                        docker rmi 35.171.158.68:8083/springapp:${VERSION}
                        '''
                        }

                    }
                }
            }
    }
}
