pipeline {
    agent { label 'node1' }

    stages {
        stage('build docker image') {
            steps {
                sh 'sudo docker build -t nginx-image .'
            }
        }
        stage('status docker') {
            steps {
                sh 'sudo docker run -d --name nginx-cont -p 90:80 nginx-image'
            }
        }
    }
}