# ECR EC2 Deploy Action

This GitHub Action automates the process of building Docker images, pushing them to Amazon ECR, and deploying them to EC2 instances.

## Usage

```yaml
- name: Deploy to ECR and EC2
  uses: CoPilot-Innovations/ecr-ec2-deploy-action@v1.0.0
  with:
    aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
    aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    aws-region: ap-southeast-2
    ecr-repository: your-repo-name
    image-tag: latest
    ec2-host: ${{ secrets.EC2_HOST }}
    ec2-user: ${{ secrets.EC2_USER }}
    ec2-private-key: ${{ secrets.EC2_PRIVATE_KEY }}
    container-name: your-container-name
    host-port: '4000'
    container-port: '5000'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `aws-access-key-id` | AWS Access Key ID | Yes | - |
| `aws-secret-access-key` | AWS Secret Access Key | Yes | - |
| `aws-region` | AWS Region | Yes | ap-southeast-2 |
| `ecr-repository` | ECR Repository name | Yes | - |
| `image-tag` | Docker image tag | No | latest |
| `ec2-host` | EC2 host address | Yes | - |
| `ec2-user` | EC2 username | Yes | - |
| `ec2-private-key` | EC2 SSH private key | Yes | - |
| `container-name` | Name for the Docker container | Yes | - |
| `container-port` | Container port to expose | No | 5000 |
| `host-port` | Host port to map | No | 4000 |

## Prerequisites

1. An AWS account with ECR repository
2. An EC2 instance with Docker installed
3. Appropriate IAM permissions
4. GitHub repository secrets configured

## Example Workflow

```yaml
name: Deploy to ECR and EC2
on:
  push:
    branches: [ "main" ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    
    - name: Deploy to ECR and EC2
      uses: CoPilot-Innovations/ecr-ec2-deploy-action@v1.0.0
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: ap-southeast-2
        ecr-repository: my-app
        image-tag: latest
        ec2-host: ${{ secrets.EC2_HOST }}
        ec2-user: ${{ secrets.EC2_USER }}
        ec2-private-key: ${{ secrets.EC2_PRIVATE_KEY }}
        container-name: my-app-container
        host-port: '4000'
        container-port: '5000'
```
