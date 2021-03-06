SRE introduction
Cloud Computing with AWS
SDLC stages
Risk factors with SDLC stages
Monitoring
Key Advantages:
Ease of use
Flexibility
Robustness
Cost

SRE introduction
- What is the role of SRE?
SREs are responsible for availability, latency, performance, efficiency, change management, monitoring, emergency response, and capacity planning.

**Cloud Computing**
- What is Cloud Computing and the benefits of using it?
Cloud computing is the delivery of computing services—including servers, storage, databases, networking, software, analytics, and intelligence—over the Internet (“the cloud”) to offer faster innovation, flexible resources, and economies of scale.
Advantages: Cost Savings, Security, Flexibility, Mobility, Insight, Increased Collaboration, Quality Control, Disaster Recovery, Loss Prevention, Automatic Software Updates,
Competitive Edge, Sustainability

**What is Amazon Web Services (AWS)**
- What is AWS and benefits of using it
AWS=the cloud platform offered by Amazon. 

Benefits: Comprehensive documentation, cost-effective, secure

**What is SDLS and stages of SDLC**
- What is SDLC and what are the stages of it
The Software Development Life Cycle (SDLC) refers to a methodology with clearly defined processes for creating high-quality software.
Stages:
1. Requirement analysis
2. Planning
3. Software design such as architectural design
4. Software development
5. Testing
6. Deployment



What are the Risk level at each stage of SDLC?
- LOW
- Medium
- High

Requirement analysis: Medium
Planning: High
Software design: Medium
Software development: Medium
Testing: Low
Deployment: Medium

What is on premise, cloud, hybrid cloud and multi cloud

On premise: data is located within your in-house servers and IT infrastructure
Cloud: A cloud-based server utilizes virtual technology to host a company’s applications offsite.
Hybrid cloud: A hybrid cloud solution is a mix of public cloud and private cloud infrastructure. Organizations might use a private cloud to store sensitive data in an on-premises or colocated data center connected by a private cloud while offloading other workloads to a public cloud service or multiple public clouds.
Multi-cloud: In a multi-cloud environment, an enterprise utilizes multiple public cloud services, most often from different cloud providers. For example, an organization might host its web front-end application on AWS and host its Exchange servers on Microsoft Azure.

Add diagram for each case with real life case examples

Pros and cons of each
 
**Provisioning**

Using Vagrant:
1. create a provision.sh on localhost
2. inject inside vagrantfile
3. with vagrant up Vagrantfile should run the script with commands we put in script
4. check in your browser 192.168.10.100

First we code in Vagrantfile: 
Vagrant.configure("2") do |config|
	config.vm.box = "ubuntu/xenial64"
	config.vm.network "private_network", ip: "192.168.10.100"
	config vm.provision "shell", path:"provision.sh" 
end

We create provision.sh on localhost. provision.sh contains:
!# /bin/bash

#Automating the installation of nginx
sudo apt-get update -y
sudo apt-get upgrade -y #sets machine up
sudo apt-get install nginx #installs nginx

Then vagrant up/ vagrant reload (if reload doesn't work use vagrant destroy and vagrant up) 
When putting the address "192.168.10.100 in browser it should display nginx page. 



**Dependencies for node app**
-install nodejs

-sudo apt-get install nodejs -y

-Ensure to install correct version
	sudo apt-get install python-software-properties
	curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
	sudo apt-get install nodejs -y

-install pm2 sudo npm install pm2 -g

-Ensure to run this inside the app folder - install npm npm install

-Launch the app npm start
-Check this 192.168.10.100:3000 on browser

**How to create a multi machine set up**
First one is created with node app provisioning
Second VM with mongodb installation
Then systemctl status mongodb

**How to configure reverse proxy** 
With nginx, we need to make the app load on ip 192.168.10.100 instead of 192.168.10.100:3000

-make sure nodejs is installed and updated (sudo apt-get install)

-open nginx configuration (file path: /etc/nginx/sites-available/default): sudo nano file path

-in the server block the following code should be added in location:

location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}

-sudo npm start 

-when entering in browser the ip address 192.168.10.100 the app should be running

