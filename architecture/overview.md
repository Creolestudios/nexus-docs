# Architecture Overview
NexusTech runs on AWS using:
- **Compute**: ECS Fargate for services, AWS Lambda for asynchronous tasks
- **Storage**: Amazon Aurora PostgreSQL, DynamoDB, Amazon S3
- **Caching**: ElastiCache Redis
- **Observability**: Amazon CloudWatch logs and metrics
