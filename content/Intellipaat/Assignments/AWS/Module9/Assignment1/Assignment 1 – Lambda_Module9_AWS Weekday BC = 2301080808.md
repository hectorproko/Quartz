
> [!info] Module 9: Lambda Assignment
> **Problem Statement:** 
> You work for XYZ Corporation. Your corporation wants to launch a new web-based application and they do not want their servers to be running all the time. It should also be managed by AWS. Implement suitable solutions. 
> 
> **Tasks To Be Performed:** 
> 1. Create a sample Python Lambda function. 
> 2. Set the Lambda Trigger as SQS and send a message to test invocations. 


%%[[Lambda_aws#Demo 1 – Lambda Function]]%%

**Setting Up and Testing an AWS Lambda Triggered by SQS**
1. **I create an SQS queue.**
   Using the steps from [[Assignment 4 – SQS And SES_Module8_AWS Weekday BC = 2301080808#|Assignment 4 – SQS And SES]], I create an SQS named `lambdaSQS` with defaults.
2. **Create the Python Lambda Function**
    - I open my preferred code editor.
    - I create a new Python file and write the following code:

```python
def lambda_handler(event, context):
    # Process the SQS messages
    for record in event['Records']:
        message = record['body']
        print(f"Received message: {message}")

    return {
        'statusCode': 200,
        'body': 'Processed the messages successfully!'
    }
```


3. **Deploying the Lambda Function on AWS**
   %%Make sure to click button deploy%%
    - I log into my AWS account.
    - I navigate to the AWS Lambda dashboard.
    - I click on "Create function".
    - I provide a name for my function `myPythonFunction`.
    - I choose Python 3.11 for the runtime.
    %%~~- I create or select an execution role with permissions to read messages from SQS.~~ ### **Permissions Info** By default, Lambda will create an execution role with permissions to upload logs to Amazon CloudWatch Logs. You can customize this default role later when adding triggers.%%
    %%Ended up having to add the policy to the role generated (see below)%%
    - Clicked "Create function"
    - I copy and paste the Python code from step 1 into the Lambda editor.
    - I click "Save" to save my function.
      
4. **Setting up the Lambda Trigger as SQS**
    
    - In the AWS Lambda dashboard, I find the "Designer" section for my function.
    - I click on "Add trigger".
      ![[Pasted image 20231011091137.png]]
    - I choose "SQS" from the list of available services.
    - I select the SQS queue I want to use.
      ![[Pasted image 20231011093004.png]]
    - Made sure "Activate trigger" was checked
    - Left default configurations.
    - Clicked "Add".
      %%whole picture[[FireShot Capture 023 - Add triggers - Lambda - us-east-1.console.aws.amazon.com.png]]%%

> [!fail]
> An error occurred when creating the trigger: The provided execution role does not have permissions to call ReceiveMessage on SQS

%%Much like in [[Assignment 3 – IAM Roles_Module3_AWS Weekday BC = 2301080808|Assignment 3 – IAM Roles]]%%

> [!tip] Solution
> For my function `myPythonFunction`, I'll update the attached role `myPythonFunction-role-me7z96sv` in the IAM console by adding the necessary permissions.
> 
> 1. **I locate the `myPythonFunction-role-me7z96sv` role.**
>     - On the IAM dashboard, I select "Roles" from the left-hand navigation pane.
>     - I find and click on `myPythonFunction-role-me7z96sv` *(role attached to my function)*.
> 2. **I attach the necessary permissions.**
>     - On the role details page, I click on the "Attach policies" button.
>     - In the search box, I can:
>         - Search for the `AWSLambdaSQSQueueExecutionRole` managed policy, which provides permissions for a Lambda function to interact with SQS.

> [!success] Successfully moved on to the next step
> ![[Pasted image 20231011105757.png]]
> *Edited the trigger made sure "Activate trigger" was checked*

![[Pasted image 20231011113245.png]]
- **Testing the Lambda Function**
    
    - I navigate to the SQS dashboard.
    - I select the queue I've set as a trigger `lambdaSQS`.
    - I click on the "Send and receive messages" button.
    - I send a sample message to the queue.
      ![[Pasted image 20231011110115.png]]
    - I wait for a moment as AWS Lambda automatically triggers upon receiving the message in SQS.
    - I then navigate to the CloudWatch logs associated with my Lambda function.
      ![[Pasted image 20231011112354.png]]
    - I confirm the print statement from my Python code displays the message I sent to the queue.

> [!success]
> ![[Pasted image 20231011132559.png]]



%%
> [!question] 
> Yes, by default, when you create a Lambda function, AWS automatically creates a new log group in Amazon CloudWatch Logs named `/aws/lambda/<function-name>` for that function. Every time your Lambda function is invoked, detailed information about the invocation is automatically recorded in CloudWatch Logs.

%%