<h1>Building and Testing a Basic Terraform Module
</h1>

<h2>Description</h2>
Terraform modules are a good way to abstract out repeated chunks of code, making it reusable across other Terraform projects and configurations. In this project, we'll be writing a basic Terraform module from scratch and then testing it out.

<br />
<br />

<img src="https://imgur.com/rjSltzM.png" height="70%" width="70%" />


<h2>Environments Used </h2>

- <b>Terraform</b>
- <b>Local Command Prompt</b>

<h2>Project walk-through:</h2>

Let's start by creating the Directory Structure for the project. 
Check that Terraform is installed and functioning properly using the terraform version command.
Create a new directory to house your Terraform code called terraform_project.
In the main project directory, create a custom directory called modules and a directory inside it called vpc. We want to keep all of our modules in one place, hence why we are making subdirectories. 
<br />
<br />
<img src="https://imgur.com/uaSeSgz.png" height="80%" width="80%">
<br />
<br />
<img src="https://imgur.com/OX1Lah6.png" height="80%" width="80%">
<br />
<br />
<img src="https://imgur.com/tbUeL6I.png" height="80%" width="80%">
<br />
<br />
Now we will write out Terraform VPC Module code. 
In the VPC directory, create a new file called main.tf and add this code.
To break it down, we are letting it know to use the AWS provider and the region specified in the 'Region' variable defined in the 'variables.tf' file we will make shortly. We are spinning up a VPC within AWS and giving it a CIDR block of 10.0.0.0/16. After creating the VPC, we are creating a subnet within the VPC with a CIDR block of 10.0.1.0./24. Finally, we are using the SSM Parameter in this code to get the AMI ID of the latest Amazon Linux 2 machine image. This will query the SSM public endpoint, which houses the ID for whatever is the latest Amazon machine Linux 2 image. 
<br />
<br />
<img src="https://imgur.com/IPfjvej.png" height="80%" width="80%">
<br />
<br />
Now we are going to create a new file called variables.tf and add this code.
We are setting the default region to 'us-east-1' in this code.
<img src="https://imgur.com/L8oS3XE.png" height="80%" width="80%">
<br />
<br />
We are going to create another new file called outputs.tf and add the code.
The Outputs code is very important. Anything that specifies as an Output can be returned back to our Terraform main code. Here we are returning two values, first being the subnet ID, and second being the AMI ID.
<br />
<br />
<img src="https://imgur.com/WYr0KWR.png" height="80%" width="80%">
<br />
<br />
So now that we are done writing our Module code, let's go over again what we just wrote. The Terraform Module is creating a VPC, a subnet, fetching the AMI ID of our image, and then returning the subnet ID and the AMI ID as outputs from the module. 
<br />
<br />
Now we can write our Main Terraform Project code
In the terraform_project directory, create a new file called main.tf and add this code, which invokes the VPC module created earlier.
<br />
<br />
<img src="https://imgur.com/rmCO1GW.png" height="80%" width="80%">
<br />
<br />
Then create a new file called outputs.tf and add the code below.
This code will basically return the private IP address of the EC2 instance being spun up via our main Terraform code. 
<br />
<br />
<img src="https://imgur.com/cU7rUPx.png" height="80%" width="80%">
<br />
<br />
Finally, we are ready to deploy and test out our new module.
Let's start by formatting the code in all of our files using the terraform fmt -recursive command, and then initialize the Terraform configuration to fetch any required providers and get the code being referenced in the module block with the terraform init command.
<br />
<br />
<img src="https://imgur.com/g69CloX.png" height="80%" width="80%">
<br />
<br />
Validate the code using the terraform validate command. This will check for syntax against the Terraform provider and make sure we are not passing any incorrect syntax or mistyped values and wrong parameters within the resources. 
<br />
<br />
<img src="https://imgur.com/5DK02oB.png" height="80%" width="80%">
<br />
<br />
Let's review the actions that will be performed when we deploy the code by using the terraform plan command and then deploy the code with the terraform apply --auto-approve command.
<br />
<br />
<img src="https://imgur.com/nEgYtWu.png" height="80%" width="80%">
<br />
<br />
Everything works! We can also view the resources that were created using the terraform state command. Also, dont forget to tear down the infrastructure using the terraform destroy command.
<br />
<br />
<img src="https://imgur.com/HQAr44v.png" height="80%" width="80%">
<br />
<br />
<h1>Thank you for reading :)<h1>
