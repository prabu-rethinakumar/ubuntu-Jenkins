# Jenkins CI-ubuntu-Cloud Foundry

## This gist narrates installation steps for Jenkins on Ubuntu to push changes to Cloud Foundry using Jenkins CI

Note:
If you are behind Firewall/proxy server ensure proxy is setup before installing the components or you may not be successful in pulling objects from registry.

setup environment variables through export 
  	
	http_proxy="http://myproxy.server.com:8080/"  
  	https_proxy="http://myproxy.server.com:8080/"  
 	HTTP_PROXY="http://myproxy.server.com:8080/"  
  	HTTPS_PROXY="http://myproxy.server.com:8080/"

Reboot the machine and login back 

Step#1: Create Jenkins server(e.g servername.xyz.com)

 	 Create your own ubuntu server using any Virtualization . If you have server of your own, login as root or admin
  

Step#2:
  Java is one of the pre-requisite for Jenkins . Install JDK or Open JDK whichever works for you
  
   		 sudo apt-get install openjdk-8-jdk openjdk-8-jre
    

Step#3: Download and install Jenkins package

 		wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
  
  		sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
  
  		sudo apt-get update
  
  		sudo apt-get install jenkins


Step#4: Jenkins User

Jenkins along with all its components are managed by user named 'jenkins' . You may have to grant this user access to all of the required components. For example - GIT


Step#5: Install Git for executing Git commands on your server (optional)
  
  		sudo apt-get install git 
  

Step#6: Status of jenkins can be checked by using below command

  		service jenkins status


Step#7: Jenkins workspace

Jenkins usually operates its workspace under var/lib/jenkins/workspace/ or installation_directory/workspace. All your projects will be managed in this folder


Step#8: This step is to enable Jenkins to push your application into Cloud Foundry using CF CLI

		wget -O cf.deb https://s3.amazonaws.com/go-cli/releases/v6.1.2/cf-cli_amd64.deb
		sudo dpkg -i cf.deb

This will download the package cf.deb and install it 

Step#9 Test CF login

	cf login -u username -p password -a http://api.xyz.com -o Org -s Space

Once logged in you are all setup for Jenkins CI 

Step#10 Log into Jenkins console using the jenkins server address on your browser. note that default port is 8080 unless you changed it during installation

	http://servername.xyz.com:8080
	
Create Users through Console . You are all set to start building your CI/CD pipelines using jenkins


Reference:
https://wiki.jenkins.io/display/JENKINS/Installing+Jenkins+on+Ubuntu





