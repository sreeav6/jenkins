First launch AWS console
------------------------------------
  a) Spin up the free tier t2.micro instance 
  b) Once it is in running state connect to that instance

Second we will be installing 
---------------------------------------
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

  c) By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open         port 8080 in the inbound traffic rules as show below.
      EC2 > Instances > Click on
      In the bottom tabs -> Click on Security Security groups
      Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All    traffic)

  d)  Login into Jenkins using the URL like below
      http://:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

  e)  Now you need to unlock the jenkins
      Run the command to copy the Jenkins Admin Password - sudo cat /var/lib/jenkins/secrets/initialAdminPassword - Enter          the Administrator password
      https://user-images.githubusercontent.com/43399466/215959008-3ebca431-1f14-4d81-9f12-6bb232bfbee3.png
      


  
