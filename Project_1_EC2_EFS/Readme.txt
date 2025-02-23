project#1: Create 3 EC2 machines with different OS and attach EFS to all 3 EC2
              1. Ec2 with Ubuntu
              2. Ec2 with Redhat Linux
              3. Ec2 with Linux

Step1: Login to AWS Management Console

Creating EC2 instances of 3 different AMI:
---------------------------------------------
Step2: Create EC2 machine with Ubuntu AMI with EC2_Ubuntu as name
    1. use default configuration of free-tier eligible resources
    2. create new security group to allow http traffic as well
    3. create a key-pair to use ssh later
Step3: Ensure EC2_Ubuntu is running

Step4: Create EC2 machine with Redhat AMI with EC2_Redhat as name
    1. use default configuration of free-tier eligible resources
    2. create new security group to allow http traffic as well
    3. create a key-pair to use ssh later
Step5: Ensure EC2_Redhat is running

Step6: Create EC2 machine with Linux AMI with EC2_Linux as name
    1. use default configuration of free-tier eligible resources
    2. create new security group to allow http traffic as well
    3. create a key-pair to use ssh later
Step7: Ensure EC2_Linux is running

Create EFS within same region as of EC2 instances:
------------------------------------------------------
Step8: Create EFS within same VPC as of EC2 instances, name it EFS_Project1
    1. EFS are Region Specific
    2. EFS should be in same VPC as of Ec2 to attach
Step9: Ensure the mount targets are ready in "Network" tab of EFS (This takes a little time, Meanwhile complete other steps)

Attach EFS on EC2_Ubuntu:
----------------------------
Step10: Connect to EC2_Ubuntu either through SSH or EC2 connect from Management Console
Step11: Install amazon-efs-utils package on EC2_Ubuntu machine by running below commands one by one
        sudo apt update
        sudo apt install -y nfs-common

Step12: Create a directory(efs_ubuntu) to mount efs by running below command
        mkdir efs_ubuntu
Step13: Ensure "efs_ubuntu" directory is created by running command "ls"
Step14: Go to EFS->View Details-> attach
        1. Copy command from "Using the NFS Client" section
        sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-0a9066376b15ea2eb.efs.us-east-1.amazonaws.com:/ efs
Step15: Go to EC2_Ubuntu CLI, paste the command and replace "efs" with directory created on EC2
        sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-0a9066376b15ea2eb.efs.us-east-1.amazonaws.com:/ efs_ubuntu
Step16: Ensure EFS is attached with EC2_Ubuntu by running below command
        df -h

        List should contain the efs mount point
Attach EFS on EC2_Redhat:
----------------------------
Step10: Connect to EC2_Redhat either through SSH or EC2 connect from Management Console
Step11: Install nfs-utils package on EC2_Redhat machine by running below commands one by one
        sudo yum update
        sudo yum install -y nfs-utils

Step12: Create a directory(EC2_Redhat) to mount efs by running below command
        mkdir EC2_Redhat
Step13: Ensure "EC2_Redhat" directory is created by running command "ls"
Step14: Go to EFS->View Details-> attach
        1. Copy command from "Using the NFS Client" section
        sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-0a9066376b15ea2eb.efs.us-east-1.amazonaws.com:/ efs
Step15: Go to EC2_Redhat CLI, paste the command and replace "efs" with directory created on EC2
        sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-0a9066376b15ea2eb.efs.us-east-1.amazonaws.com:/ EC2_Redhat
Step16: Ensure EFS is attached with EC2_Redhat by running below command
        df -h

        List should contain the efs mount point
Attach EFS on EC2_Linux:
----------------------------
Step10: Connect to EC2_Linux either through SSH or EC2 connect from Management Console
Step11: Install nfs-utils package on EC2_Linux machine by running below commands one by one
        sudo yum update
        sudo yum install -y nfs-utils

Step12: Create a directory(EC2_Linux) to mount efs by running below command
        mkdir EC2_Linux
Step13: Ensure "EC2_Linux" directory is created by running command "ls"
Step14: Go to EFS->View Details-> attach
        1. Copy command from "Using the NFS Client" section
        sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-0a9066376b15ea2eb.efs.us-east-1.amazonaws.com:/ efs
Step15: Go to EC2_Linux CLI, paste the command and replace "efs" with directory created on EC2
        sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-0a9066376b15ea2eb.efs.us-east-1.amazonaws.com:/ EC2_Linux
Step16: Ensure EFS is attached with EC2_Linux by running below command
        df -h

        List should contain the efs mount point