### Deploys a high-availability web app using CloudFormation
    deploy web servers for a highly available web app using CloudFormation
    The network diagram 'High_Availability_Architecture.jpeg' gives a blue print 
    of the setup we will be implementing using cloudformatio

#### LoadBalancer DNSto access our webApp

    http://serve-webse-zyutvapa3ci3-1598211026.us-east-1.elb.amazonaws.com/

#### networkInfra.yml
    This template deploys a VPC, with a pair of public and private subnets spread 
    across two Availabilty Zones. It deploys an Internet Gateway, with a default 
    route on the public subnets. It deploys a pair of NAT Gateways (one in each AZ), 
    and default routes to them in the private subnets.

#### serverInfra.yml
    Deploys two (2) EC2 instances running Apache webservers in each of our Private subnets in the two (2) AZs, 
    an Auto Scaling group to manage the instance count using a launch configuration
    the launch configuration provided in this template uses the ubuntu 18 ami with apache server installed
    An Elastic Load Balancer ELB is also deployed to manage traffic between our web servers, as well as perform health checks 

#### Getting started
    Firstly open project in a code editor or terminal
    configure aws using the access key and secrete key by entering the commands below

aws configure 

    N:B set the region equals to the region specified in both the create.sh and update.sh scripts
    to successfully create all stack, First run the 'networkInfra.yml' and its matching parameter 'network-parameters.json' to deploy and provision the underlining network our web servers would use. Type the command below

./create.sh *stacknameofchoice* networkInfra.yml network-parameters.json

    check the console to verify stack creation completion or type the command below in the terminal

aws cloudformation describe-stacks 

    Next, we can create/provision our servers by running the 'serverInfra.yml' and its matching 'server-parameters.json'. Run the command below

./create.sh *stacknameofchoice* serverInfra.yml server-parameters.json

    verify stack creation by typing below command. We should see both our network and server stacks created successfully

aws cloudformation describe-stacks
