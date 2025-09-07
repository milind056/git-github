pipeline {
    agent any

    parameters {
        choice(name: 'ACTION', choices: ['start', 'stop'], description: 'Start or stop the EC2 instance')
    }

    environment {
        AWS_REGION = 'us-east-1'
        INSTANCE_ID = 'i-0123456789abcdef0'
        AWS_CREDENTIALS_ID = 'aws-credentials'
    }

    stages {
        stage('Control EC2 Instance') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: "${env.AWS_CREDENTIALS_ID}"]]) {
                    script {
                        if (params.ACTION == 'start') {
                            sh """
                            aws ec2 start-instances --instance-ids ${env.INSTANCE_ID} --region ${env.AWS_REGION}
                            """
                        } else if (params.ACTION == 'stop') {
                            sh """
                            aws ec2 stop-instances --instance-ids ${env.INSTANCE_ID} --region ${env.AWS_REGION}
                            """
                        }
                    }
                }
            }
        }
    }
}
