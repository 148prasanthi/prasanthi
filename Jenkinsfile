pipeline {
    agent any

    stages {
        stage('aws-s3') {
            agent {
                docker {
                    image 'amazon/aws-cli'
                    args "--entrypoint=''"
                }
            }
            environment {
                s3_bucket_name = 'prasanthi-test'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'aws-creds', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                  sh '''
                    aws --version
                    echo 'hello s3!' > index.html
                    aws s3 cp index.html s3://$s3_bucket_name/index.html
                  '''
                }
            }
        }
    }
}