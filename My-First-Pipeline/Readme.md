First launch AWS console
------------------------------------
  a) Spin up the free tier t2.micro instance 
  b) Once it is in running state connect to that instance

Second we will be installing Java and Jenkins
----------------------------------------------
  a) We will installing pre-requisities for Jenkins that is java jdk
  Install Java:
  
    sudo apt update
    sudo apt install openjdk-11-jre
	
  Verify Java is installed or not
  	java -version
    
  b) We will installing Jenkins now
  
    curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt-get update
    sudo apt-get install jenkins

  c) By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS.Openport 8080 in the inbound traffic rules as show below.
      EC2 > Instances > Click on
      In the bottom tabs -> Click on Security Security groups
      Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All    traffic)

  d)  Login into Jenkins using the URL like below
      http://:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

  e)  Now you need to unlock the jenkins
      Run the command to copy the Jenkins Admin Password - 
      
      sudo cat /var/lib/jenkins/secrets/initialAdminPassword - Enter the Administrator password

  f) As we are using docker as a agent we have to install docker pipeline as a pulgin in jenkins
  
	1. Login into Jenkins
 	2. Click on Manage jenkins and then click on Manage pulgins 
  	3. In the Avaliable pulgins search for Docker Pipeline
   	4. Select the Docker pipeline pulgin and click on install
    	5. Restart jenkins after pulgin is installed
  	6. Wait for the jenkins to be restarted
   
   g) Now we will do Docker Slave configuration, Run the below commands in your EC2 instance
   
	sudo apt update
	sudo apt install docker.io
 
   h) We will grant the ubuntu user and jenkins user permission to docker deamon
	
 	sudo su - 
	usermod -aG docker jenkins
	usermod -aG docker ubuntu
	systemctl restart docker

   i) Once you are done with the above steps, it is better to restart Jenkins.
   
  	http://<ec2-instance-public-ip>:8080/restart
      


  
