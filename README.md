# Configure-VPC-Flow-Logs-and-Store-Logs-in-S3-Using-IAM-Role-
This project demonstrates how to set up VPC Flow Logs to monitor network traffic within a VPC and securely store the logs in a dedicated Amazon S3 bucket. Access permissions are managed using an IAM role, adhering to the principle of least privilege.
# Objective
The main objective is to establish a robust logging solution for network traffic by:
. Enabling VPC Flow Logs on a specified VPC.
. Configuring an S3 bucket as the log destination.
. Creating a custom IAM role with a trust policy that allows the VPC Flow Logs service to write to the S3 bucket.
# Prerequisites
An active AWS account.
Basic understanding of AWS services, including VPC, S3, and IAM.
An existing VPC to monitor (or create a new one).
# Step-by-Step Setup Instructions
Step 1: Create an S3 Bucket
Create a new S3 bucket to store the log files.
Navigate to the S3 service in the AWS Console.
Click Create bucket.
Provide a unique bucket name (e.g., vpc-flow-logs-bucket-your-id) and choose your preferred AWS Region.
