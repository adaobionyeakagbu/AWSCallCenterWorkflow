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
The workflow calls one AWS Lambda function to create a support case, invokes another function to assign the case to a support representative for resolution, and so on. It also passes data between Lambda functions to track the status of the support case as it's being worked on. 
A state machine needs to be created. A state machine execution is an instance of your workflow, and occurs each time a Step Functions state machine runs and performs its tasks. Each Step Functions state machine can have multiple simultaneous executions, which you can initiate from the Step Functions console (which is what you will do next), or by using AWS SDKs, Step Functions API actions, or the AWS CLI. An execution receives JSON input and produces JSON output.

First, I created a state machine by selecting 'Workflow by code'. 
Then I inputed the JSON code that constitutes the Amazon State Language used in creating the workflow, and selected the role I created previously.
The workflow will follow a sequence of tasks and choices that look like the image below:
![2023-05-04 23 04 40](https://user-images.githubusercontent.com/66325142/236330598-1aa75361-f0e5-4443-b60b-af5998d1432f.png)

### Step 3: Create Lambda functions
I navigated to Lambda and created 5 functions that will open a case, assign a case to an agent, work on cases, close cases and escalate cases.
![2023-05-04 23 21 57](https://user-images.githubusercontent.com/66325142/236333468-e17fe561-2a98-4c5a-8d08-ffed75500bc7.png)
Pasted the code and deployed the function.
![2023-05-04 23 26 30](https://user-images.githubusercontent.com/66325142/236333792-5e6c31a1-cd51-423a-bdc8-52de00b44c82.png)

### Step 4: Populate workflow
Next, I had to edit the Step Function State Machine code to recognize my lambda functions for each task. This can be simply done in the workflow studio by selecting the task you want to edit and choosing the right function.
![2023-05-04 23 34 02](https://user-images.githubusercontent.com/66325142/236335283-bab51b97-7a9e-4b47-b5f9-a209fd8d4d0f.png)

Then you can apply and exit, and save the workflow.

### Step 5: Execute workflow
The serverless workflow is now ready to be executed. A state machine execution is an instance of your workflow, and occurs each time a Step Functions state machine runs and performs its tasks. Each Step Functions state machine can have multiple simultaneous executions, which you can initiate from the Step Functions console (which is what you will do next), or by using AWS SDKs, Step Functions API actions, or the AWS CLI. An execution receives JSON input and produces JSON output.
![2023-05-04 23 43 43](https://user-images.githubusercontent.com/66325142/236336513-5745315a-29b2-4e0c-93a7-7680c32ec635.png)

Yaay! The workflow coordinated all of my functions according to the logic defined, and passed data from one state to another, which meant I didn’t need to write that code into each individual function.
