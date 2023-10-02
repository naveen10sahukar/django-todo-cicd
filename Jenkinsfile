pipeline {
    agent any
    
    tools {
        jdk "jdk17"
        maven "maven3"
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'develop', url: 'https://github.com/naveensahukar10/django-todo-cicd.git'
            }
        }
        
        stage('Docker Build') {
            steps {
                sh "docker build -t django-todo ."
            }
        }
        
        stage('Docker Tag') {
            steps {
                sh "docker tag django-todo naveensahukar/django-todo:latest"
            }
        }
        
        stage('Docker Push') {
            steps {
                script {
                   withDockerRegistry(credentialsId: 'DockerHub', toolName: 'docker') {
                    sh "docker push naveensahukar/django-todo:latest"
                   }
                }
            }
        }
        
        stage('Deploy Application') {
            steps {
                sh "docker run -d -p 8000:8000 --name django-todo-container naveensahukar/django-todo:latest"
            }
        }
    }
}
