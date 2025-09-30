pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        ECR_REPO = '123456789012.dkr.ecr.us-east-1.amazonaws.com/myapp'
        IMAGE_TAG = "${env.BUILD_ID}"
        CLUSTER = 'my-ecs-cluster'
        SERVICE = 'my-ecs-service'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/your-user/ecs-jenkins-sample-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $ECR_REPO:$IMAGE_TAG ."
                }
            }
        }

        stage('Login to ECR') {
            steps {
                script {
                    sh "aws ecr get-login-password --region $AWS_DEFAULT_REGION | docker login --username AWS --password-stdin $ECR_REPO"
                }
            }
        }

        stage('Push to ECR') {
            steps {
                script {
                    sh "docker push $ECR_REPO:$IMAGE_TAG"
                }
            }
        }

        stage('Deploy to ECS') {
            steps {
                script {
                    sh """
                    aws ecs update-service \
                      --cluster $CLUSTER \
                      --service $SERVICE \
                      --force-new-deployment \
                      --region $AWS_DEFAULT_REGION
                    """
                }
            }
        }
    }
}
