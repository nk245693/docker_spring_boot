pipeline {
    agent any

    environment {
        registry = "public.ecr.aws/y7f3w2i5/mydockerrepo /var/lib/jenkins/workspace/project-eks"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: ' https://github.com/nk245693/docker_spring_boot.git']])
            }
        }
        
        stage ("Build JAR") {
            steps {
                sh "mvn clean install"
            }
        }
        
        stage ("Build Image") {
            steps {
                script {
                    sh "pwd"
                    docker.build -t spring_boot .
                }
            }
        }
        
        stage ("Push to ECR") {
            steps {
                script {
                    sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/y7f3w2i5/mydockerrepo"
                    sh "docker push public.ecr.aws/y7f3w2i5/mydockerrepo /var/lib/jenkins/workspace/project-eks:latest"
                    
                }
            }
        }
        
        /*stage ("Helm package") {
            steps {
                    sh "helm package springboot"
                }
            }
                
        stage ("Helm install") {
            steps {
                    sh "helm upgrade myrelease-21 springboot-0.1.0.tgz"
                }
            }*/
    }
}
