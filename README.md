# Configure-VPC-Flow-Logs-and-Store-Logs-in-S3-Using-IAM-Role-
This project demonstrates how to set up VPC Flow Logs to monitor network traffic within a VPC and securely store the logs in a dedicated Amazon S3 bucket. Access permissions are managed using an IAM role, adhering to the principle of least privilege.
#Objective
The main objective is to establish a robust logging solution for network traffic by:

Enabling VPC Flow Logs on a specified VPC.

Configuring an S3 bucket as the log destination.

Creating a custom IAM role with a trust policy that allows the VPC Flow Logs service to write to the S3 bucket.

#Prerequisites
An active AWS account.

Basic understanding of AWS services, including VPC, S3, and IAM.

An existing VPC to monitor (or create a new one).

#Step-by-Step Setup Instructions
Step 1: Create an S3 Bucket
Create a new S3 bucket to store the log files.

Navigate to the S3 service in the AWS Console.

Click Create bucket.

Provide a unique bucket name (e.g., vpc-flow-logs-bucket-your-id) and choose your preferred AWS Region.

Step 2: Create an IAM Role
Create an IAM role that the VPC Flow Logs service can assume to write logs to your S3 bucket.

Go to the IAM service and click Roles, then Create role.

Choose Custom trust policy and paste the following JSON:

JSON

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "vpc-flow-logs.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
Click Next.

On the "Add permissions" page, click Create policy.

In the new tab, paste the following permissions policy, replacing the bucket name:

JSON

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "s3:PutObject"
            ],
            "Effect": "Allow",
            "Resource": "arn:aws:s3:::your-vpc-flow-logs-bucket/AWSLogs/*"
        }
    ]
}
Name the policy (e.g., vpc-flow-logs-s3-write-policy) and create it.

Return to the role creation tab, refresh the policies list, and attach the newly created policy to your role.

Name the role (e.g., VPCFlowLogsRole) and create it.

Step 3: Enable VPC Flow Logs
Enable flow logs on your VPC, pointing them to the S3 bucket and IAM role.

Go to the VPC service.

Select Your VPCs, then choose the VPC you want to monitor.

Go to the Flow Logs tab and click Create flow log.

Set the Destination to S3 bucket, and enter the S3 bucket ARN.

Select the IAM role you created from the dropdown menu.

Click Create flow log.

#Verification
To verify that the setup is working:

Generate some network traffic within your VPC (e.g., by launching an EC2 instance or connecting to an existing one).

After a few minutes, check your S3 bucket. You should see new folders with a structured path like s3://vpc-flow-logs-bucket/AWSLogs/<account-id>/....

Download and open a .gz file. The log entries will be space-separated and contain information about the network traffic, including source/destination IPs, ports, and the action taken (ACCEPT or REJECT).
