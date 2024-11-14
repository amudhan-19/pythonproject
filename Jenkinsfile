pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/Thivagar1494/k8s-proj.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t pyimage /var/lib/jenkins/workspace/k8sproj'
                sh 'sudo docker tag pyimage thivagarrajad/pyimage:latest'
                sh 'sudo docker tag pyimage thivagarrajad/pyimage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push thivagarrajad/pyimage:latest'
                sh 'sudo docker image push thivagarrajad/pyimage:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/k8sproj/pod.yaml'
                sh 'sudo kubectl rollout restart deployment k8s-pod'
            }
        }
    }
}
