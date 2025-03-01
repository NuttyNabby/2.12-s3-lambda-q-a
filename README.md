# 2.12-s3-lambda-q-a

**1. What is the purpose of the execution role on the Lambda function?**

The execution role is an IAM role that grants permissions for the Lambda function to interact with other AWS services. Specifically, it allows the function to:

- Read from S3 (if processing files from S3).
- Write logs to Amazon CloudWatch for monitoring and debugging.
- Access other AWS services if needed (e.g., DynamoDB, SNS, SQS).

Without the necessary permissions in the execution role, the Lambda function cannot perform actions like reading or writing to an S3 bucket.

**2. What is the purpose of the resource-based policy on the Lambda function?**

A resource-based policy on a Lambda function controls which AWS accounts and services can invoke the function.

In the case of an S3-triggered Lambda, the resource-based policy:

- Allows Amazon S3 to invoke the Lambda function when new files are created.
- Specifies which S3 bucket has permission to trigger the function.

Without this policy, S3 cannot trigger the Lambda function, even if the function has execution permissions.

**3. If the function needs to upload a file into an S3 bucket, what changes are needed?**
🔹 Update to the Execution Role
- Add s3:PutObject permission to allow the Lambda function to upload files to the target S3 bucket.
- Optionally, add s3:ListBucket if the function needs to verify bucket contents.

🔹 Resource-Based Policy (If Needed)
- If the Lambda function is just uploading files, no additional resource-based policy is needed.
- However, if another AWS service or account needs to invoke the Lambda function, update the resource-based policy to allow that service to invoke it.
