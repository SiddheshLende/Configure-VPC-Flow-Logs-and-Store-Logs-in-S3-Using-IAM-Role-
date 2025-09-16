# Configure-VPC-Flow-Logs-and-Store-Logs-in-S3-Using-IAM-Role-
This project demonstrates how to set up VPC Flow Logs to monitor network traffic within a VPC and securely store the logs in a dedicated Amazon S3 bucket. Access permissions are managed using an IAM role, adhering to the principle of least privilege.
# Objective
The main objective is to establish a robust logging solution for network traffic by:
. Enabling VPC Flow Logs on a specified VPC.
. Configuring an S3 bucket as the log destination.
. Creating a custom IAM role with a trust policy that allows the VPC Flow Logs service to write to the S3 bucket.
