# AWS Parsec Gaming Rig

Last Update - 2020/02/12

It is a CloudFormation template which will deploy 6 different EC2 Launch Templates, using the Pasec official build AMI at AWS.

## Gaming Rig Specification:
The price of different instance type depends on which region you have deployed.
 - g2.2xlarge
	 - NVIDIA GRID K520 GPU
	 - 8 vCPU
	 - 15 GiB RAM
	 - Hourly Price: $0.767 - $1.16
	 - *I'm not even sure can you launch this type, it too old.*
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
	 - ***Not available in Singapore region***

## Available Region
You can go [https://www.cloudping.info](https://www.cloudping.info) to check which region has the lowest latency.
 - us-east-1 (US N.Virginia)
 - us-west-1 (US N.California)
 - eu-west-1 (Ireland)
 - ap-southeast-1 (Signapore)
 - ap-northeast-1 (Tokyo)

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
  `https://s3-ap-southeast-1.amazonaws.com/miklet.pro/assets/cloudformation-template/aws-parsec-gaming-rig.yaml`
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
11. Click 'Connect' and enter the password 4ubg9sde
12. And now you should be able to see your instance destop.
13. Login the Parse, and do some config
14. AND LET THE GAMES BEGIN, ENJOY

### AWS On-Demand vs Spot Instance
I won't talk much here, if you want to know what is the detail difference, google it.
#### [On-Demand](https://aws.amazon.com/ec2/pricing/on-demand/)
- Pay the compute capacity you have consumed.
- Launched instance won't terminate by it self.
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
You have deploy and launch a g4dn.xlarge On-Demand instance at 2020/01/02 16:00, and terminate the instance at 2020/01/15 22:00, and you have played 3 hours per day.
The network data transfer(IO) used 100GB at total.


    Instance:
    $0.894/Hour * 3Hours/Day * 14Days = $37.548
    Bandwidth:
    $0.01/GB * 100GB = $1
    Storage:
    $0.1/M * 100GB * ((14D * 24h/d - 16h - 2h) * 60m/h * 60s/m) / 86400s/d / 30d/M = $4.416
    (M=Month,D=Day,h=Hour,m=Minute,s=Second)
    Total = $37.548 + $1 + $4.416 = $42.964
    
