## PROJECT 2

# AUTOMATION OF ELITE CORPORATION AWS EC2 INSTANCE INFRASTRUCTURE USING TERRAFORM.

## Project Scope and Available Resources:
This project is about Elite Corporation, who desire to automate an AWS EC2 instance infrastructure, which will bring about speed in installation, and error free deployment. The tool to bring about this automation is Terraform, which is an Infrastructure as Code tool.
Requirements:
1.	The instance will run on Ubuntu and should be on a specified region.
2.	Use variables instead of hardcoding by using Terraform state management for AWS region, key pair name, and instance type. 
3.	After applying Terraform Code, check the Terraform state to verify that the infrastructure is being tracked.
4.	Modify the instance type, re-apply the configuration, and destroy the infrastructure using Terraform.


Documentation

1.	Go to AWS and get the following:
a.	Region (for this project use us-east-2 as default)

b.	Pick on Ubuntu through create instance to get the AMI (amazon machine image).

c.	Get the instance type (use t2.micro for this project).

d.	Create a key pair name (use key-elitecorp for this project)




![img](img/img1.png)




![img](img/img2.png)




![img](img/img3.png)




![img](img/img4.png)




2.	Open a folder this project (for this project use Elitecorp)




![img](img/img5.png)




3.	Open VS code in the folder, and create three files in the Elitecorp folder: main.tf, variables.tf, and terraform.tfvars.




![img](img/img6.png)




4.	On file one, main.tf write instructions telling Terraform what to create. Note these are not hard coded they are all variables. These instructions are to tell terraform to create the instance, suggesting the region, key pair, instance type. But the AMI and the tag are named. This means the tag and the AMI are not variables.




![img](img/img7.png)




5.	Here, variable.tf file. The variables stated in the file main.tf are assigned their values, but on default.




![img](img/img8.png)




6.	 This file, terraform.tfvars is optional, but vital. Here, values of resources attached to infrastructure are stated (hardcoded). The reason for it being optional is, the setup can run withou it, but the good side of it is, you can easily make adjustments here without altering the set up.




![img](img/img9.png)




7.	On the terminal ```terraform init``` is imputed to start the process, then ```terraform plan```, and ```terraform apply``` command. After apply we see Apply complete! Resources: 1 change, 0 added, 0 destroyed.




![img](img/img10.png)




![img](img/img11.png)




![img](img/img12.png)




![img](img/img13.png)




![img](img/img14.png)




![img](img/img15.png)




8.	Elite corporation AWS EC2 instance created, with t2.micro as the type of instance.




![img](img/img15a.png)




9.	```Terraform show``` command. To check the infrastructure state.




![img](img/img16.png)




![img](img/img17.png)




10.	Instance type modified from t2.micro to t2.medium on the terraform.tfvars file.




![img](img/img18.png)




11.	Command process- ```Terraform plan``` command and ```terraform apply```.
12.	Plan applied, we see Apply complete! Resources: 0 added,1 changed, 0 destroyed.




![img](img/img19.png)




13.	Elite corporation AWS EC2 instance type has changed to t2.medium




![img](img/img20.png)




14.	Apply ```terraform destroy``` command




![img](img/img21.png)




15.	Infrastructure destroyed. It is easily seen destroy complete! Resources: 1 destroyed.




![img](img/img22.png)

