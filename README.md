# HHA504-E2E-FINAL

**1. Setup and deploy EC2**

### Ubuntu Server 18.04 LTS (HVM), SSD Volume Type - 64-bit (x86)
### Instance type: t2.micro
### Storage size: 20 GiB

### Added 2 security group rules**
        - Type: SSH, MySQL/Aurora
        - Port Range: 22, 3306
        - Source: Anywhere 0.0.0.0/0/ Anywhere 0.0.0.0/0
        - Master instance name: sk_master1_server

**2. Create a user to the ubuntu EC2 instance**

### Username: skclient
### Password: ahi2021

**3. Install mySQL on master instance**

### Open Mac Terminal and change working directory to Downloads (location of .pem file)
        - cd Downloads
### copy/paste SSH client to terminal
        - ssh -i "sayeda_test_scratch.pem" ubuntu@ec2-3-144-198-23.us-east-2.compute.amazonaws.com
### Update operating system
        - # sudo apt-get update
### Create new user in OS without .pem key requirement
        - # sudo adduser skclient
        (New UNIX password: ahi2021)
### Change sshd_config setting to allow external users to log in with a password (without a pem key) using in text editor nano
        - # sudo nano /etc/ssh/sshd_config
        (Locate line: “PasswordAuthentication no” and change no to yes)
        [Control^] + O to save
        [Control^] + x to exit
### Restart SSH to push change
        - # sudo service ssh restart
        [Control^] + D and log out of remote server and log back in as Ubuntu user: skclient
        (Ssh skclient@3.144.198.23 | Password: ahi2021)
