# CloudFormation AWS Infrastructure

Provisions EC2, S3, and Security Group using AWS CloudFormation (IaC) — tested locally with LocalStack.

## What it provisions

- **EC2 Instance** (t2.micro) with Security Group attached
- **S3 Bucket** for application storage
- **Security Group** allowing HTTP (80) and SSH (22)

## Stack Deploy (LocalStack)

```bash
# Start LocalStack
docker run -d --name localstack-cfn -p 4566:4566 \
  -e SERVICES=ec2,s3,cloudformation localstack/localstack:3.0

# Deploy stack
aws --endpoint-url=http://localhost:4566 cloudformation create-stack \
  --stack-name my-infra-stack \
  --template-body file://infra.yaml

# Verify
aws --endpoint-url=http://localhost:4566 cloudformation describe-stacks \
  --stack-name my-infra-stack
```

## Parameters

| Parameter | Default | Options |
|---|---|---|
| EnvironmentName | dev | dev, staging, prod |
| InstanceType | t2.micro | any EC2 type |

## Outputs

- S3 Bucket Name
- Security Group ID  
- EC2 Instance ID
