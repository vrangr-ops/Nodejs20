Navigate to website -  https://sparta-devops.signin.aws.amazon.com/console

Enter login credentials

# Launching an EC2 instance

\*The section below concerns the configuration setting for an EC2 instance.

## Name 

-  Follow appropriate convention. e.g. organization-name-project.

## Application and OS Images

- Select ubuntu LTS image 64bit x86.

## Instance type 

- t3 micro

## Select SSH key

(see comments below)

## Network

- Name security group. e.g. organization-name-project-sg

**Configure security group by selecting ==edit== option.**

- SSH, source type =custom, source =0.0.0.0/0, port range= 22
- Custom TCP, source type =custom, source =0.0.0.0/0, port range =3000
- HTTP, source type =custom, source =0.0.0.0/0, port range =80![20ef80ae58949d53c3157ee459d902e8.png](../_resources/20ef80ae58949d53c3157ee459d902e8-4.png)

## Configure storage

- 1Gb,Gp3

**With the setting above the EC2 instance can be launched.**

* * *

## Connecting to EC2 via SSH

\*Prerequisites - have SSH client e.g. Gitbash installed if using widows.

https://git-scm.com/install/

1.  Open an SSH client. Ensure directory is in /.ssh folder
2.  Navigate to connect to instance
3.  <img src="../_resources/08bfc33ab14cc25a8526c23b68825038-4.png" alt="08bfc33ab14cc25a8526c23b68825038.png" width="367" height="235">
4.  Select SSH connection
5.  `run chmod 400 "se-name-key-pair.pem"`
6.  run command
7.  `ssh -i "se-name-key-pair.pem" ubuntu@ec2-3-255-106-70.eu-west-1.compute.amazonaws.com`

* * *

## Installing nginx 

Use Bash terminal (gitbash)

### Update packages

`Sudo apt update -y`

### Upgrade packages

`sudo apt upgrade -y`

## Install nginx

1.  `sudo apt install nginx -y`
2.  `sudo systemctl restart nginx`
3.  `sudo systemctl status nginx`

\# enable nginx - to make it start up on boot

- `sudo systemctl enable nginx`
- Test http connection- select open adress
    1.  ![0f8ba57853f94d7c25ea3d45ea161aed.png](../_resources/0f8ba57853f94d7c25ea3d45ea161aed-4.png)

## Deploying Nodejs to EC2

1.  Download the compressed nodejs file. `nodejs20-se-test-app-2025.zip`
2.  Use bash terminal (gitbash) to navigate to folder containing nodejs folder.
3.  Use scp to move file to EC2 instance. Ensure the EC2 public IP is correct.
4.  `scp -i ~/.ssh/se-name-key-pair.pem ./nodejs20-se-test-app-2025.zip ubuntu@3.248.229.243:~`

## Install nodejs v20

1.  open bash terminal in EC2 instance
2.  `sudo bash -c "curl -fsSL https://deb.nodesource.com/setup_20.x | bash -"`
    
3.  `sudo apt install -y nodejs`

Check version- `node -v`

## Running nodejs app

1.  Install unzip in EC2 instance
2.  `sudo apt install unzip -y`
    
3.  Extract files
4.  `sudo unzip nodejs20-se-test-app-2025`
5.  Navigate to app folder
6.  `cd nodejs20-se-test-app-2025/app`
    
7.  To run the nodejs app, execute the command below
    
8.  `npm install`
    
9.  `npm start`

&nbsp;

# Comments

- The SSH key is provided by the cloud provider and used for authenticating.
- Keep the SSH key in the /home/.ssh folder.

&nbsp;
