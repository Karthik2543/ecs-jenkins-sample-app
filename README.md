# ECS Jenkins Sample App

This is a simple Flask app containerized with Docker, deployed to AWS ECS using Jenkins pipeline.

## Steps
1. Push this repo to GitHub
2. Create an ECR repo (AWS CLI or Console)
3. Update `Jenkinsfile` with:
   - ECR repo URL
   - ECS cluster name
   - ECS service name
4. Create Jenkins pipeline job → "Pipeline from SCM"
5. Run pipeline → App will deploy to ECS
