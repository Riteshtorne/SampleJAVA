pipeline {
    agent any
    environment {
        IMAGE_NAME = "demo-app"
    }
    stages {
        stage('Checkout') {
            steps {
                // Use credentials and specify branch
                git(
                    url: 'https://github.com/Riteshtorne/SampleJAVA.git',
                    credentialsId: 'Github',  // GitHub username + PAT
                    branch: 'main'
                )
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl apply -f deployment.yaml
                kubectl apply -f service.yaml
                kubectl apply -f hpa.yaml
                '''
            }
        }
    }
}
