AWS Lambda EC2 Tagging Script
Overview
This script enhances your company's resource management by automatically attaching an "owner" tag to newly created AWS services. It leverages AWS Lambda, triggered by Amazon EventBridge, to automate the tagging process, ensuring that every new service instance can be easily identified by its owner.

Key Components
Amazon EventBridge: Utilized for triggering the Lambda function based on specific events.
AWS CloudTrail: Integrated to capture API activities and log them to Amazon CloudWatch, aiding in the monitoring and auditing of AWS resource manipulations.
IAM Role: A specifically crafted IAM role that grants the necessary permissions for the Lambda function to execute actions, including reading and writing API activities and tagging resources.
Implementation Details
The workflow starts with EventBridge, which monitors for specific API calls indicating the creation of a new service instance. Upon detection, it triggers the Lambda function. For capturing these events, CloudTrail is configured to log API calls to CloudWatch. The Lambda function, written in Python and utilizing the Boto3 library, then tags the newly created EC2 instance with the owner's information.

Steps:
Enable CloudTrail logging to CloudWatch for API activity monitoring.
Create an IAM role with permissions to read and write API activities, as well as to tag EC2 instances.
Configure an EventBridge rule to trigger the Lambda function based on EC2 instance creation events captured by CloudTrail.
Implement the Lambda function using Boto3 to tag the EC2 instance with the owner's name.
Issues Faced and Resolutions
A significant challenge was related to permissions. Initially, the Lambda function lacked the necessary permissions to tag EC2 instances. This was resolved by modifying the execution role associated with the Lambda function:

Navigate to the Lambda function's configuration page and locate the execution role section.
Edit the policy to include permissions for tagging EC2 instances.
Select the EC2 service, choose tagging actions, and specify the resources as "all resources".
Review and save the policy changes to ensure the Lambda function has the appropriate permissions.
Conclusion
By automating the tagging of AWS resources, this script streamlines the management and identification of service instances, enhancing governance and accountability within your AWS environment.