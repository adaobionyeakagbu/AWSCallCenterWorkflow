# AWSCallCenterWorkflow
This project uses AWS Step Functions to design and run a serverless workflow that coordinates multiple AWS Lambda functions to automate handling of support tickets in a call center.
Step Functions is a serverless orchestration service that lets you easily coordinate multiple Lambda functions into flexible workflows that are easy to debug and change. AWS Lambda is a compute service that lets you run code without provisioning or managing servers.

## What this project will accomplish:

- Create a Step Functions state machine to describe the current call center process
- Create a few simple Lambda functions that simulate the tasks of the support team
- Pass data between each Lambda function to track the progress of the support case
- Perform several tests of your workflow to observe how it responds to different inputs
- Delete the AWS resources you used in the tutorial

### Step 1: Create AWS Identity and Access Management (IAM) role
An IAM role that allows Step Functions to access Lambda was created by navigating to the IAM service on my AWS management console and clicking on Roles. To create a role, I selected AWS Service as the 'Trusted Entity Type', 'Step Functions' as the use case, named the role, and left all others as default.

### Step 2: Create a state machine and serverless workflow
