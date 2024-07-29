// pipeline {
//     agent { label 'node1' }

//     stages {
//         stage('build docker image') {
//             steps {
//                 sh 'sudo docker build -t nginx-image .'
//             }
//         }

//         stage('remove docker container') {
//             steps {
//                 sh 'sudo docker rm -f nginx-cont'
//             }
//         }
//         stage('status docker') {
//             steps {
//                 sh 'sudo docker run -d --name nginx-cont -p 90:80 nginx-image'
//             }
//         }
//     }
// }

pipeline {
    agent { label 'node1' }

    stages {
        stage('build docker image') {
            steps {
                sh 'sudo docker build -t nginx-image .'
            }
        }
        stage('remove docker container') {
            steps {
                sh 'sudo docker rm -f nginx-cont'
            }
        }
        stage('status docker') {
            steps {
                sh 'sudo docker run -d --name nginx-cont -p 90:80 nginx-image'
            }
        }
    }

    post {
        always {
            script {
                def snsTopicArn = 'arn:aws:sns:us-east-1:862066027316:jenkins'
                def message = "The pipeline has completed with status: ${currentBuild.currentResult}"
                def subject = "Pipeline Notification: ${currentBuild.fullDisplayName}"
                
                withAWS(region: 'us-east-1', credentials: 'aws-credentials-id') {
                    snsPublish(topicArn: snsTopicArn, message: message, subject: subject)
                }
            }
        }
    }
}
