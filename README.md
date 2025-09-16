# Configure-VPC-Flow-Logs-and-Store-Logs-in-S3-Using-IAM-Role-
This project demonstrates how to set up VPC Flow Logs to monitor network traffic within a VPC and securely store the logs in a dedicated Amazon S3 bucket. Access permissions are managed using an IAM role, adhering to the principle of least privilege.
# Objective
The main objective is to establish a robust logging solution for network traffic by:  
Enabling VPC Flow Logs on a specified VPC.  
Configuring an S3 bucket as the log destination.  
Creating a custom IAM role with a trust policy that allows the VPC Flow Logs service to write to the S3 bucket.  
# Prerequisites  
An active AWS account.  
Basic understanding of AWS services, including VPC, S3, and IAM.  
An existing VPC to monitor (or create a new one).  
# Step-by-Step Setup Instructions  
Step 1: Create an S3 Bucket     
1. Create a new S3 bucket to store the log files.  
2. Navigate to the S3 service in the AWS Console.  
3. Click Create bucket.  
4. Provide a unique bucket name (e.g., vpc-flow-logs-bucket-your-id) and choose your preferred AWS Region.  

Step 2: Create an IAM Role
Create an IAM role that the VPC Flow Logs service can assume to write logs to your S3 bucket.
1. Go to the IAM service and click Roles, then Create role.  
2. Choose Custom trust policy and paste the following JSON: (json_policy1)
3. Click Next.
4. On the "Add permissions" page, click Create policy.
5. In the new tab, paste the following permissions policy, replacing the bucket name: (json_policy2)
6. Name the policy (e.g., vpc-flow-logs-s3-write-policy) and create it.
7. Return to the role creation tab, refresh the policies list, and attach the newly created policy to your role.
8. Name the role (e.g., VPCFlowLogsRole) and create it.

Step 3: Enable VPC Flow Logs  
Enable flow logs on your VPC, pointing them to the S3 bucket and IAM role.  
1. Go to the VPC service.
2. Select Your VPCs, then choose the VPC you want to monitor.
3. Go to the Flow Logs tab and click Create flow log.
4. Set the Destination to S3 bucket, and enter the S3 bucket ARN.
5. Select the IAM role you created from the dropdown menu.
6. Click Create flow log.

#Verification
To verify that the setup is working: 
1. Generate some network traffic within your VPC (e.g., by launching an EC2 instance or connecting to an existing one).  
2. After a few minutes, check your S3 bucket. You should see new folders with a structured path like s3://vpc-flow-logs-bucket/AWSLogs/<account-id>/....
3. Download and open a .gz file. The log entries will be space-separated and contain information about the network traffic, including source/destination IPs, ports, and the action taken (ACCEPT or REJECT).  
