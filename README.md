# HHA504-E2E-FINAL

**1. Setup and deploy EC2**

> Ubuntu Server 18.04 LTS (HVM), SSD Volume Type - 64-bit (x86)
> Instance type: t2.micro
> Storage size: 20 GiB

> Added 2 security group rules**
        - Type: SSH, MySQL/Aurora
        - Port Range: 22, 3306
        - Source: Anywhere 0.0.0.0/0/ Anywhere 0.0.0.0/0
        - Master instance name: sk_master1_server

**2. Create a user to the ubuntu EC2 instance**

- Username: skclient
- Password: ahi2021
