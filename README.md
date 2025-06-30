# cost-optimization
A simple automation script to read today’s Jenkins build logs and upload them to an S3 bucket using the AWS CLI. Ideal for backup, audit, or log retention purposes.
This project provides a lightweight Shell script to automatically collect daily Jenkins build logs and upload them to an Amazon S3 bucket. Designed for DevOps teams looking to maintain offsite backups of CI/CD pipeline logs with minimal setup. Uses AWS CLI for seamless integration with S3.

Project Title:
Jenkins CI/CD Logs — Automate Cost‑Efficient Log Archiving

Short Description:
A DevOps-friendly script to streamline daily Jenkins (or other CI/CD) build logs, filter relevant data, and upload them to AWS S3—minimizing cloud storage costs through FinOps best practices.

What This Project Solves:

🎯 Cost Optimization: Reduce the size and retention span of CI logs to lower S3 storage expenses 


⚙️ Automation: Fully script-driven—no manual handling—using shell or Python and AWS CLI.

🗓️ Daily Archival: Automatically harvest today’s build logs, compress or filter them, and push to S3.

Tools used for this Project:

Jenkins (build logs files)

AWS S3 archival

CI/CD cost control

Shell scripting + AWS CLI

Firstly, jenkins should be installed in your machine (if not installed then run this below commands in your machine)

Install Jenkins.
Pre-Requisites:

Java (JDK)
Run the below commands to install Java and Jenkins
Install Java

```
sudo apt update
sudo apt install openjdk-17-jre
```
Verify Java is Installed

```
java -version
```

Now, you can proceed with installing Jenkins
```
 curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee 
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] 
 https://pkg.jenkins.io/debian binary/ | sudo tee \
   /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

**Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.

EC2 > Instances > Click on

In the bottom tabs -> Click on Security

Security groups

Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic).

![image](https://github.com/user-attachments/assets/2f36a928-16be-4c7f-953a-a5886ef0e194)


Login to Jenkins using the below URL:

http://:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

Note: If you are not interested in allowing All Traffic to your EC2 instance 1. Delete the inbound traffic rule for your instance 2. Edit the inbound traffic rule to only allow custom TCP port 8080

After you login to Jenkins, - Run the command to copy the Jenkins Admin Password - `sudo cat /var/lib/jenkins/secrets/initialAdminPassword` - Enter the Administrator password

![image](https://github.com/user-attachments/assets/bfd5fa28-8f29-4270-9751-8eab620f18df)


Click on Install suggested plugins
![image](https://github.com/user-attachments/assets/37d144cc-f87a-4172-83d3-a1b3cd9092d4)


Wait for the Jenkins to Install suggested plugins
![image](https://github.com/user-attachments/assets/cbfd6870-2a80-4b4d-81db-de5daf5ac43e)


Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]

![image](https://github.com/user-attachments/assets/4d22a887-462e-4937-8700-989e0af38476)

Jenkins Installation is Successful. You can now starting using the Jenkins

![image](https://github.com/user-attachments/assets/e7b06b7a-7d74-4f12-8a81-5d6c28744ef2)

Install the Docker Pipeline plugin in Jenkins:

Log in to Jenkins.

Go to Manage Jenkins > Manage Plugins.

In the Available tab, search for "Docker Pipeline".

Select the plugin and click the Install button.

Restart Jenkins after the plugin is installed.

![image](https://github.com/user-attachments/assets/178d33ef-2944-4a70-a1df-70ce415467d9)

Wait for the Jenkins to be restarted.


```
http://<ec2-instance-public-ip>:8080/restart
```

Install AWS CLI (v2)
To use this script, you need the AWS CLI installed on your machine. Follow the steps below to install it:

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

```
aws --version
```

Create an AWS IAM User:
To interact with AWS programmatically, you should create an IAM (Identity and Access Management) user with appropriate permissions. Here's how to create one:

a. Log in to the AWS Management Console with an account that has administrative privileges.

b. Navigate to the IAM service.

c. Click on "Users" in the left navigation pane and then click "Add user."

Choose a username, select "Programmatic access" as the access type, and click "Next: Permissions."

Attach policies to this user based on your requirements. At a minimum, you should attach the "AmazonEC2FullAccess" policy for basic EC2 operations. If you need access to other AWS services, attach the relevant policies accordingly.

Review the user's configuration and create the user. Be sure to save the Access Key ID and Secret Access Key that are displayed after user creation; you'll need these for Terraform.

Configure AWS CLI Credentials:
Use the AWS CLI to configure your credentials. Open a terminal and run:
```
aws configure
```
It will prompt you to enter your 

AWS Access Key ID

Secret Access Key

default region

default output format

Enter the credentials you obtained in the previous step.

![image](https://github.com/user-attachments/assets/e107ffd1-8eb0-4936-a00c-4a5809ab1f15)


![Screenshot from 2025-06-28 13-14-57](https://github.com/user-attachments/assets/2a6a2ba5-6cfc-4728-9d98-913805a3df00)

![image](https://github.com/user-attachments/assets/7d143b61-399c-40d3-9b77-6be201d3daf6)


![image](https://github.com/user-attachments/assets/13ef02fa-902d-4e40-8c40-4e943f214d75)


