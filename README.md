# Devops-Project-1
Devops Project 1

The project Mainly is about simple ci/cd config with jenkins, which would cd the code from github to aws ec2 instance,
For the project we are deploying a Javascript game to the webserver/ec2instance.

- <b> Work Flow </b>
- ![devops-project-1 drawio (1)](https://user-images.githubusercontent.com/53990452/177825384-4c508e4f-2ce4-4e59-8a04-610c4549dac6.png)

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


2) Setting up Github WebHooks :
- for the example we are using git repo : https://github.com/Saumil343/test1.git
- Go to settings of your respective repo
- Go to webhooks
- Add web Hook
- And in the payload section add: http://public_ip_of_jenkins_Server:8080/github-webhook/
- Content Type : application/json
- Select : Push Events
- And click create webhook
- EXAMPLE:
![image](https://user-images.githubusercontent.com/53990452/177816425-c3caa4d3-d506-4597-bfae-96b7f14ef82e.png)


4) Installing Jenkins pluggin
- Go to jenkins dashboard
- GO to manage jenkins
- manage plugins
- and search for "Publish Over SSH" & install it

5) Setting up over webserver[where we want to deploy our app] in jenkins machine :
- Go to jenkins dashboard
- Go manage jenkins
- GO to Cofigure System
-  Scroll down to publish over ssh section
-  and add a webserver there
-  set the name and add the public ip along with the username to login to the server
-  EXAMPLE:
-  ![image](https://user-images.githubusercontent.com/53990452/177818212-448ca6c5-2168-4386-bb83-789ea2588a95.png)
- save it
- click advance option and select use different key
- paste your private instance key which was used while creating the instance
- EXAMPLE :
- ![image](https://user-images.githubusercontent.com/53990452/177818552-81653565-c7e5-4575-97f8-3ef4155d4827.png)
- That's it our Server is ready to be used.

7) Creating Continious Integration Job
- Go to Dashboard
- create new item and give it a name and select Free Style Project
- Go to general section and scroll to Source Code Management Section and select git and add your git repo link of the project to be deployed.
- EXAMPLE
![image](https://user-images.githubusercontent.com/53990452/177819185-2e169902-5f0d-43a5-887d-02f13759d2cc.png)
- Scroll and add build triggers and select GitHub hook trigger for GITScm polling.
- EXAMPLE
- ![image](https://user-images.githubusercontent.com/53990452/177819421-1e0c9080-b845-4091-94a4-a89b54e378b6.png)
- Scroll and add POST BUILD ACTION and give a name of Continious deployment job[yet to be created]
- Example
- ![image](https://user-images.githubusercontent.com/53990452/177819619-145f1db2-6565-4aff-a975-5b506e735787.png)

8) Creating Continious Deployment Job.
- Go to Dashboard
- create new item and give it a name and select Free Style Project
- Go to build trigger and build env
- add our webserver machine and add exec command as shown below: 
- here we are using a shell script for the bettter execution!
- ![image](https://user-images.githubusercontent.com/53990452/177820075-77529ecb-45ce-4c22-a288-f88fe2be730b.png)
- ![image](https://user-images.githubusercontent.com/53990452/177820083-b9ddcaf7-f2ac-4234-94de-6f18119c8f09.png)
- ![image](https://user-images.githubusercontent.com/53990452/177820090-550d9f8b-1d23-443f-bf2a-86fa320ca38f.png)
- ![image](https://user-images.githubusercontent.com/53990452/177820092-e720f258-0384-4d44-90ff-fa3a66d65eeb.png)

9) The Shell Script Used
- #!/bin/bash
- sudo yum install httpd -y
- sudosystemctlstarthttpd
- sudo cd /var/www/html/ 
- sudo rm -rf test1
- sudo git clone https://github.com/Saumil343/test1.git
- sudo rm -rf /var/www/html/*
- sudo mv test1/* /var/www/html/
- sudo systemctl enable httpd
- sudo systemctl restart httpd
- ![image](https://user-images.githubusercontent.com/53990452/177820978-95e91f54-944d-4916-9fb4-7c5928864cd5.png)

10) <b> And thus we can see now as soon as we push or change something in our github repo the changes are refled and are hosted over our web server which can be accessed over the public ip of the server in any browser </b>


