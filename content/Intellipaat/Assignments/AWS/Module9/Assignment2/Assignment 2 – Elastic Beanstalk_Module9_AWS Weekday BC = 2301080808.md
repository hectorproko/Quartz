==Pending CleanUP==
 #AWS

> [!info] Module 9: Elastic Beanstalk Assignment
> **Problem Statement:** 
> You work for XYZ Corporation. Your corporation wants to launch a new web-based application and they do not want their servers to be running all the time. It should also be managed by AWS. Implement suitable solutions. 
> 
> **Tasks To Be Performed:** 
> 1. Create an Elastic Beanstalk environment with the runtime as PHP. 
> 2. Upload a simple PHP file to the environment once created.

%%
[[Elastic Beanstalk_aws#Demo 2 – Beanstalk]]

> [!fail]- Issue
> 
> <br>![[Pasted image 20231012142752.png]]
> Got this issue again seem realated to the RDS issue which was caused by the VPC, 
> 
> > [!tip] Solution
> > used a new none Default vpc
> 

This is the part I used different VPC
[[myVPC used Beanstalk.png]]
%%

`index.php` ^6f66a7
```php
<?php
  echo "Hello, World! Today's date is " . date('Y-m-d') . ".";
?>
```

^e77287

### Step 1: Create a New Elastic Beanstalk Environment

1. I open my browser and log into the AWS Management Console.
2. In the search bar at the top, I type "Elastic Beanstalk" and then select it from the dropdown list to access the service.
3. On the Elastic Beanstalk dashboard, I click on the "Create application" button.

4. In the "Environment tier", I ensure "Web server environment" is selected.
    
5. In the "Application Information" section:
    - I input my desired application name "PHP-App".
      
6. Under "Environment information":
    - I name my environment, perhaps "PHP-App-env".
    - In the "Domain" section, I stick with the auto-generated option.
      
7. In the "Platform" section:
    - I confirm "Managed platform" is chosen for "Platform type".
    - I ensure "PHP" is selected from the "Platform" dropdown.
    - I choose my desired PHP version from the "Platform branch" dropdown. "PHP 8.2 running on 64bit Amazon Linux 2".
    - I leave the "Platform version" as the recommended version
      
8. In the "Application code" section:
    - I'll pick "Sample application", for now and deploy my code later.
    
9. In the "Presets" section:
    - I left it "Single instance".
      
10. Once I've filled everything, I'll click "Next" and "Skip to review" button and "Submit" to set up the environment.

<br>![[Pasted image 20231012150425.png]]

### Deploying My Code to Elastic Beanstalk:

1. I clicked my environment, `PHP-App-env-env`.
   <br>![[Pasted image 20231012150827.png]]
2. I clicked on `Upload and deploy`.
   <br>![[Pasted image 20231012150857.png|450]]
3. I chose my file, `index.zip`, and uploaded it.
4. I named this upload `PHP-App-env-version-1`.
5. I pressed `Deploy` and waited for it to finish.
6. After deploying, I tested my PHP page by visiting the provided domain: `PHP-App-env-env-eba-nsk8y8bp.us-east-1.elasticbeanstalk.com`.

<br>![[Pasted image 20231012151043.png]]

I've successfully set up an AWS Elastic Beanstalk environment running PHP and deployed my simple PHP application.



%%

> [!attention]
> make sure you pick public subnet if your EC2 is hoting page

> [!attention]- Had issue with custom VPC `MyVPC`
> Here it works when using the Default VPC
> Had an issue with MyVPC custom VPC that was fixed
> [[Project 2 – Website Orchestration_Projects_AWS Weekday BC = 2301080808#^6aff71|Project 2 – Website Orchestration Issue]]

%%





