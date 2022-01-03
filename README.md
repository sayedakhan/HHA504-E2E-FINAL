#### HHA504-E2E-FINAL

### 1. Setup and deploy EC2

    ## Ubuntu Server 18.04 LTS (HVM), SSD Volume Type - 64-bit (x86)
    ## Instance type: t2.micro
    ## Storage size: 20 GiB

    ## Added 2 security group rules
        - Type: SSH, MySQL/Aurora
        - Port Range: 22, 3306
        - Source: Anywhere 0.0.0.0/0/ Anywhere 0.0.0.0/0
        - Master instance name: sk_master1_server

### 2. Create a user in the ubuntu EC2 instance
    With the following credentials:
        - Username: skclient
        - Password: ahi2021
    
    ## Open Mac Terminal and change working directory to Downloads (location of .pem file)
        - cd Downloads
    ## copy/paste SSH client to terminal
        - ssh -i "sayeda_test_scratch.pem" ubuntu@ec2-3-144-198-23.us-east-2.compute.amazonaws.com
    ## Update operating system
        - # sudo apt-get update
    ## Create new user in OS without .pem key requirement
        - # sudo adduser skclient
        (New UNIX password: ahi2021)
    ## Change sshd_config setting to allow external users to log in with a password (without a pem key) using in text editor nano
        - # sudo nano /etc/ssh/sshd_config
        (Locate line: “PasswordAuthentication no” and change no to yes)
        [Control^] + O to save
        [Control^] + x to exit
    ## Restart SSH to push change
        - # sudo service ssh restart
    ## [Control^] + D and log out of remote server and log back in as Ubuntu user: skclient to confirm change
        - (Ssh skclient@3.144.198.23 | Password: ahi2021)
    ## Log out and log in as Ubuntu admin: ssh -i "sayeda_test_scratch.pem" ubuntu@ec2-3-144-198-23.us-east-2.compute.amazonaws.com

### 3. Install mySQL on master instance
       - # sudo apt install mysql-server mysql-client
    ## Log into MySQL environment 
       - # sudo mysql
       
### 4. Create a user in MySQL that can access all databases
       - # create user  ‘skdba’@’%’  identified by ‘ahi2021’;
    ## Set credentials > Username: skdba, Password: ahi2021
    ## Confirm with command: # select user from mysql.user;
    ## Grant all privileges to user skdba
       - # grant all privileges on  *.* to ‘skdba’@’%’ with grant option;
    ## Confirm with command: # show grants for skdba;

### 5. Create database called e2e
    ## Log out as MySQL user 
    ## Log in as ubuntu user skclient and change bind-address from 127.0.0.1 to 0.0.0.0 to allow external connections
       - # sudo nano etc/mysql/mysql.conf.d/mysql.cnf
       (Locate line: "bind address 127.0.0.1" and change to 0.0.0.0)
       [Control^] + O to save
       [return] to write file
       [Control^] + x to exit
    ## Restart MySQL to push change
       - # sudo service mysql restart
    ## Log into MySQL
       - # sudo mysql
       Create database e2e
   
### 6. Write a python script that connects to your SQL install and create a 'h1n1' table in the e2e database with dataset H1N1 and Seasonal Flu Vaccines


    ## import pandas as pd 
    ## import sqlalchemy
    ## from sqlalchemy import create_engine

    ## FluVaccine = pd.read_csv('/Users/sayedakhan/Downloads/H1N1_Flu_Vaccines.csv', index_col=False, delimiter = ',')

    ## MYSQL_HOSTNAME = '3.144.198.23'
    ## MYSQL_USER = 'skdba'
    ## MYSQL_PASSWORD = 'ahi2021'
    ## MYSQL_DATABASE = 'e2e'

    ## connection_string = f'mysql+pymysql://{MYSQL_USER}:{MYSQL_PASSWORD}@{MYSQL_HOSTNAME}:3306/{MYSQL_DATABASE}'
    ## engine = create_engine(connection_string)

    ## TABLENAME = 'h1n1'

    ## FluVaccine.to_sql(TABLENAME, con=engine)

### 7. Create a dump (.sql) file
    
    ## Connect to remote server
    - # ssh -i "sayeda_test_scratch.pem" ubuntu@ec2-3-144-198-23.us-east-2.compute.amazonaws.com
    - # sudo mysqldump --databases e2e > backup.sql
    
### 8. Move dump (.sql) file from remote server to local machine

    ## Open 2 terminals: 1 terminal for remote machine, 2nd for local machine
    ## Enter the following command in terminal of local machine
    - # scp skclient@ec2-3-144-198-23.us-east-2.compute.amazonaws.com:/home/ubuntu/backup.sql /Users/sayedakhan/Downloads
    ## Confirm file in downloads folder > file name: backup.sql, size: 11.4 mb, pathname: /Users/sayedakhan/Downloads/backup.sql
    ## Open file using visual studio code






   

