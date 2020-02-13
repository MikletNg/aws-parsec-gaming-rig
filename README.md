# AWS Parsec Gaming Rig

`Last Update - 2020/02/13`

It is a CloudFormation template which will deploy 6 different EC2 Launch Templates, using the Pasec official build AMI at AWS.

## Why Cloud Gaming?
You can play any AAA games on any device with a browser without buying an expensive gaming machine. Also, you can enjoy the endless compute capacity on the Cloud.

![Origin Apex Legend Downlaod Speed](https://i.imgur.com/7RxosO3.png)

## Gaming Rig Specification
The price of different instance type depends on which region you have deployed.
 - g2.2xlarge
	 - NVIDIA GRID K520 GPU
	 - 8 vCPU
	 - 15 GiB RAM
	 - Hourly Price: $0.767 - $1.16
 - g3.4xlarge
	 - NVIDIA Tesla M60 GPU
	 - 16 vCPU
	 - 122 GiB RAM
	 - Hourly Price:  $1.14 - $2.316
 - g4dn.xlarge
	 - NVIDIA T4 GPU
	 - 4 vCPU
	 - 16 GiB RAM
	 - Hourly Price:  $0.526 - $0.894
	 - ***Not available in Singapore and Sydney region***
 - g4dn.2xlarge
	 - NVIDIA T4 GPU
	 - 8 vCPU
	 - 32 GiB RAM
	 - Hourly Price:  $1.12 - $1.1383
	 - ***Not available in Singapore and Sydney region***
 - g4dn.4xlarge
	 - NVIDIA T4 GPU
	 - 16 vCPU
	 - 64 GiB RAM
	 - Hourly Price:  $1.94 - $2.361
	 - ***Not available in Singapore and Sydney region***

## Available Region
You can go [https://www.cloudping.info](https://www.cloudping.info) to check which region has the lowest latency.
 - us-east-1 (US N.Virginia)
 - us-west-1 (US N.California)
 - us-west-2 (US Oregon)
 - eu-central-1 (DE Frankfurt)
 - eu-west-1 (Ireland)
 - ap-southeast-1 (Signapore)
 - ap-southeast-2 (AU Sydney)
 - ap-northeast-1 (JP Tokyo)

## TL;DR
1. Create an AWS account
2. Select the region
3. Create case to AWS for allowing you to use G type instance.
4. After approved, deploy the CloudFormation stack using the template below
	
	`https://aws-parsec-gaming-rig.s3.ap-east-1.amazonaws.com/template.yaml`
5. Go to EC2 Launch Template and select which instance type you want to launch
6. After launched, wait the status check success
7. Use TightVNC to connect to the instance, by using INSTANCE_IP_ADDRESS::5900 and the password is *4ubg9sde*
8. Login tu your Parsec and do some configuration

## Set Up
**This section will NOT start/launch any EC2 instance(s).**
**NO money will cost during and after this section**
1. [Register an AWS account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)
2. **YOU WON'T ABLE TO START ANY GPU INSTANCES IF YOU MISS THIS STEP**
    1. At default, all new created AWS account will not be able to launch any G instance, which you need to create a support case to AWS.
    2. Go [AWS Support Dashboard - Create Case](https://console.aws.amazon.com/support/cases#/create?issueType=service-limit-increase&limitType=ec2-instances)
    3. At the 'Requests' section, select the region you wish to use.
    4. Select 'All G Instance'
    5. Enter any number into 'New limit value', this value has limit HOW MANY instance you can launch, if you wish to launch ony ONE, just enter 1.
    6. At the 'Use case description', just enter what you want, like '*I want to increase All G instance limit to 1*'
    7. then just wait, AWS Support may take few minutes or hours (worese will be a day) to 
    3. Select the lowest latency region on the top right corner.
4. Go to [CloudFormation](https://console.aws.amazon.com/cloudformation/)
5. Click 'Create Stack' > 'with new resources'
6. Paste the following URL into 'Amazon S3 Url'
  
	`https://aws-parsec-gaming-rig.s3.ap-east-1.amazonaws.com/template.yaml`
 7. Enter the stack name - *AWSParsecGamingRig*
 8. Next > Next > Create Stack
 9. Wait until the stack create complete.

## Launch a Gaming Rig
1. After you have finish *Set Up*, go [AWS EC2 Launch Template](https://console.aws.amazon.com/ec2/v2/home#LaunchTemplates:)
2. Select the instance type you wish to launch.
3. Click 'Actions' > 'Launch instance from template' ('Actions' button at the top right)
4. Scroll down to the bottom, click 'Launch instance from template'
5. Go [EC2 Running Instance](https://console.aws.amazon.com/ec2/v2/home#Instances:sort=instanceState)
6. You should see the instance that running, wait the 'Status Check' to become '2/2', it should take few minutes.
7. While waiting the instance ready, go download and install [TightVNC](https://www.tightvnc.com/download.php)
8. After the instance ready, note down the Public IP Address
9. Open 'TightVNC Viewer' and.
10. Enter your IP address and add '::5900' behind. (Example: 12.34.56.78::5900)
11. Click 'Connect' and enter the password *4ubg9sde*
12. And now you should be able to see your instance destop.
13. Login the Parse, go 'Setting' > 'Host'
14. Set the 'Bandwidth Limit' to '50 Mbps', and set 'H.265 (HEVC)' to 'On'
15. AND LET THE GAMES BEGIN, ENJOY

### AWS On-Demand vs Spot Instance
I won't talk much here, if you want to know what is the detail difference, google it.

#### [On-Demand](https://aws.amazon.com/ec2/pricing/on-demand/)
-	Pay the compute capacity you have consumed.
-	Launched instance won't terminate by it self.

#### [Spot](https://aws.amazon.com/ec2/spot/)
-	Has up to 90% discount compare to On-Demand prices
-	It may terminate any moment. You can go [Spot Instance Advisor](https://aws.amazon.com/ec2/spot/instance-advisor/) and check how is the possibility will AWS terminate/stop your instance.
-	Maximum launch time - 6 hours

## Cost
It depends on which instance type and class you have choose.

There are multitple things will cost your money.
- Computer (EC2 Instance)
	- You launch it, it starts billing.
	- You stop it, it stop billing
	- Go check [On-Demand Pricing](https://aws.amazon.com/ec2/pricing/on-demand/) or [Spot Pricing](https://aws.amazon.com/ec2/spot/pricing/)(Select the corresponding region and Windows not Linux)
- Storage (EBS)
	- Go check [EBS Pricing](https://aws.amazon.com/tw/ebs/pricing/)

### Example
You decide to launch your Parsec Gaming Rig at us-east-1 (US N. Virginia).
You have deployed and launched a g4dn.xlarge On-Demand instance at 2020/01/02 16:00, and terminate the instance at 2020/01/15 22:00, and you have played 3 hours per day.
The network data transfer(IO) used 100GB at total.

    Instance:
    $0.71/Hour * 3Hours/Day * 14Days = $27.69
    Bandwidth:
    $0.01/GB * 100GB = $1
    Storage:
    $0.1/M * 100GB * ((14D * 24h/d - 16h - 2h) * 60m/h * 60s/m) / 86400s/d / 30d/M = $4.416
    (M=Month,D=Day,h=Hour,m=Minute,s=Second)
    Total = $27.69 + $1 + $4.416 = $33.106
    
## Tips
- ***!!!WARMING!!! THIS IS A TEMORARY STORAGE, WHICH MEANS IT WILL ALL DISAPEAR AFTER SHUTDOWN*** If you have launched an G4 instance, you should have an NVMe SSD storage (125GB/225GB). Go check this [tutorial](https://www.diskpart.com/windows-10/windows-10-disk-management-0528.html) to know how to alocate that volume.
- If you want to install some famous applications quicklym you can use ***Chocolatey***.
	
	`Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`
	
	`choco install googlechrome origin uplay -y`
	
	The command above install chocolatey, Google Chrome, Origin and Uplay.
	Kindly remind, do not forget to run powershell as administrator.