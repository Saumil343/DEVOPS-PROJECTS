# Devops-Project-1
Devops Project 1

The project Mainly is about simple ci/cd config with jenkins, which would cd the code from github to aws ec2 instance,
For the project we are deploying a Javascript game to the webserver/ec2instance.

<b> Steps Followed </b>


1) Create and Setup Jenkins On AWS EC2 Instance.
-  Create a ec2 instance with amazon linux 2 ami
-  To Install Jenkins :
- sudo yum update all -y
- sudo yum install jenkins -y
- sudo systemctl start jenkins
- sudo systemctl status jenkins
- Now We can see jenkins is installed and open the console by going on public_ip_of_instance:8080
- Get secret key by : sudo cat /var/lib/jenkins/secrets/initialAdminPassword
- Now make a new Jenkins user and setup the username and password
-  Jenkins Installed and working!.

2) Setting up our jenkins job.
- We will have to setup 2 jenkins jobs: 1) For Continious Integration 2) Continious Deployment
- ![image](https://user-images.githubusercontent.com/53990452/177814763-d4888c95-a2d9-4f76-8700-abc86b9ff08d.png)

