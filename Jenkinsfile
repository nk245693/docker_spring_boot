pipeline {
    agent any

    environment {
        registry = "505716311492.dkr.ecr.us-east-1.amazonaws.com/testcluster"
    }
    stages {
        stage('Checkout') {
            steps {
                sh "echo clone stage"
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: ' https://github.com/nk245693/docker_spring_boot.git']])
            }
        }
        
        stage ("Build JAR") {
            steps {
                sh "mvn clean install"

            }
        }
        
      /*  stage ("Build Image") {
            steps {
                script {
                    dockerImage = docker.build registry
                      dockerImage.tag("$BUILD_NUMBER")

                }
            }
        }
        
        stage ("Push to ECR") {
            steps {
                script {
                    sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 505716311492.dkr.ecr.us-east-1.amazonaws.com"
                    sh " docker push 505716311492.dkr.ecr.us-east-1.amazonaws.com/testcluster:latest"
                }
            }
        }
        
        stage ("Helm deploy") {
            steps {
                      sh "helm upgrade first --install mychart --namespace helm-deployment --set image.tag=$BUILD_NUMBER"
                }
            }
                
        
    }
}
