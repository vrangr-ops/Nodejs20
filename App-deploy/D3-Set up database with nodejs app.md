## Deploying a mongodb database to an EC2 instance

- \*The section below concerns the configuration setting for an EC2 instance.

<div class="joplin-table-wrapper"><table border="1" style="border-collapse: collapse; width: 100.008%;" class="jop-noMdConv"><colgroup class="jop-noMdConv"><col style="width: 49.9587%;" class="jop-noMdConv"><col style="width: 49.9587%;" class="jop-noMdConv"></colgroup><thead class="jop-noMdConv"><tr class="jop-noMdConv"><th scope="col" class="jop-noMdConv"><p><span class="jop-noMdConv" style="color: rgb(255, 255, 255);"><span style="font-weight: bolder;" class="">Name</span></span></p><ul style="font-weight: 400;" class="jop-noMdConv"></ul></th><th scope="col" class="jop-noMdConv"><span style="font-weight: 400; background-color: rgb(16, 21, 26);" class="">Follow an appropriate convention. e.g. organization-name-project title.</span></th></tr></thead><tbody class="jop-noMdConv"><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="font-weight: bold;" class="">Application and OS Images</span></td><td class="jop-noMdConv"><p>Select ubuntu LTS image 64bit x86.</p></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="font-weight: bolder; background-color: rgb(16, 21, 26);" class="">Instance type</span></td><td class="jop-noMdConv"><p>t3 micro</p></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="font-weight: bolder;" class="">Select SSH key</span></td><td class="jop-noMdConv">See comments section below</td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><p><strong class="jop-noMdConv">Network</strong></p><p><em class="jop-noMdConv">Configure security group by selecting <mark class="jop-noMdConv">edit</mark> option.</em></p></td><td class="jop-noMdConv"><p>Name security group. e.g. organization-name-project-sg</p><ul class="jop-noMdConv"><li class="jop-noMdConv">SSH, source type =custom, source =0.0.0.0/0, port range= 22</li><li class="jop-noMdConv">Custom TCP, source type =custom, source =0.0.0.0/0, port range =27017</li></ul></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="font-weight: bolder;" class="">Configure storage</span></td><td class="jop-noMdConv"><ul class="jop-noMdConv"><li class="jop-noMdConv">1Gb,Gp3</li></ul></td></tr></tbody></table></div>

**With the setting above the EC2 instance can be launched.**

## Connecting to EC2 via SSH

\*Prerequisites - have SSH client e.g. Gitbash installed if using widows.

https://git-scm.com/install/

1.  Open an SSH client. Ensure directory is in /.ssh folder
2.  Navigate to connect to instance
3.  <img src="../../_resources/08bfc33ab14cc25a8526c23b68825038.png" alt="08bfc33ab14cc25a8526c23b68825038.png" width="367" height="235" class="jop-noMdConv">
4.  Select SSH connection
5.  `run chmod 400 "se-name-key-pair.pem"`
6.  run command
7.  `ssh -i "se-name-key-pair.pem" ubuntu@ec2-3-255-106-70.eu-west-1.compute.amazonaws.com`

&nbsp;

## Install mongodb

1.  sudo apt install gnupg curl -y
    
2.  Download mongodb
    
3.  `curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | \`  
                            `   sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg \`  
                            `   --dearmor`
    
4.  `sudo apt update -y`
    
5.  &nbsp;`echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list`  
    `deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse`
    
6.  `sudo apt update`
    
7.  `sudo apt install -y mongodb-org=7.0.6 mongodb-org-database=7.0.6 mongodb-org-server=7.0.6 mongodb-mongosh=2.1.5 mongodb-org-mongos=7.0.6 mongodb-org-tools=7.0.6`
    
8.  `mongod --version` to check correct version installed
    
9.  `sudo systemctl status mongod`
    

**To allow the nodejs app to connect with the database the mongodb config file needs to be edited.**

1.  `cd /etc`
    
2.  <span style="color: rgb(0, 91, 71);">ls</span>
    
3.  <span style="color: rgb(0, 91, 71);">sudo nano mongod.conf</span>
    
4.  Change the bind_Ip values to 0.0.0.0
    
5.  <span style="color: rgb(0, 91, 71);">cat mongod.conf</span>
    
6.  <span style="color: rgb(0, 91, 71);">sudo chown -R mongodb:mongodb /var/lib/mongodb</span>
    
7.  `sudo chown mongodb:mongodb /tmp/mongodb-27017.sock`
    
8.  <span style="color: rgb(0, 91, 71);">sudo service mongod restart</span>
    
9.  `sudo systemctl status mongod`
    

## Deploying nodejs app

### Launching an EC2 instance

- \*The section below concerns the configuration setting for an EC2 instance.

<div class="joplin-table-wrapper"><table border="1" style="border-collapse: collapse; width: 100.008%;" class="jop-noMdConv"><colgroup class="jop-noMdConv"><col style="width: 49.9587%;" class="jop-noMdConv"><col style="width: 49.9587%;" class="jop-noMdConv"></colgroup><thead class="jop-noMdConv"><tr class="jop-noMdConv"><th scope="col" class="jop-noMdConv"><p><span class="jop-noMdConv" style="color: rgb(255, 255, 255);"><span style="font-weight: bolder;" class="">Name</span></span></p><ul style="font-weight: 400;" class="jop-noMdConv"></ul></th><th scope="col" class="jop-noMdConv"><span style="font-weight: 400; background-color: rgb(16, 21, 26);" class="">Follow an appropriate convention. e.g. organization-name-project title.</span></th></tr></thead><tbody class="jop-noMdConv"><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="font-weight: bold;" class="">Application and OS Images</span></td><td class="jop-noMdConv"><p>Select ubuntu LTS image 64bit x86.</p></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="font-weight: bolder; background-color: rgb(16, 21, 26);" class="">Instance type</span></td><td class="jop-noMdConv"><p>t3 micro</p></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="font-weight: bolder;" class="">Select SSH key</span></td><td class="jop-noMdConv">See comments section below</td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><p><strong class="jop-noMdConv">Network</strong></p><p><em class="jop-noMdConv">Configure security group by selecting <mark class="jop-noMdConv">edit</mark> option.</em></p></td><td class="jop-noMdConv"><p>Name security group. e.g. organization-name-project-sg</p><ul class="jop-noMdConv"><li class="jop-noMdConv">SSH, source type =custom, source =0.0.0.0/0, port range= 22</li><li class="jop-noMdConv">Custom TCP, source type =custom, source =0.0.0.0/0, port range =3000</li><li class="jop-noMdConv">HTTP, source type =custom, source =0.0.0.0/0, port range =80</li></ul></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="font-weight: bolder;" class="">Configure storage</span></td><td class="jop-noMdConv"><ul class="jop-noMdConv"><li class="jop-noMdConv">1Gb,Gp3</li></ul></td></tr></tbody></table></div>

**With the setting above the EC2 instance can be launched.**

* * *

## Connecting to EC2 via SSH

1.  Open an SSH client. Ensure directory is in /.ssh folder
2.  Navigate to connect to instance
3.  <img src="../../_resources/08bfc33ab14cc25a8526c23b68825038.png" alt="08bfc33ab14cc25a8526c23b68825038.png" width="367" height="235" class="jop-noMdConv">
4.  Select SSH connection
5.  `run chmod 400 "se-name-key-pair.pem"`
6.  run command
7.  `ssh -i "se-name-key-pair.pem" ubuntu@ec2-3-255-106-70.eu-west-1.compute.amazonaws.com`

To run nodejs script

2.  `sudo nano app-deploy.sh`
    
3.  Copy script and save
    
4.  Make script executable by changing permissions
    
5.  `sudo chmod +x app-deploy.sh`
    
6.  `./app-deploy.sh`
    
7.  Link the database to the nodejs app by making sure the public ip of the database is correct. e.g. `3.252.140.103`
    
8.  `export DB_HOST=mongodb://3.252.140.103:27017/posts`
    

## Launch the nodejs app

1.  `cd se-sparta-test-app /app`
    
2.  kill any processes which may interfere
    
3.  `pm2 kill`
    
4.  `node seeds/seed.js`
    
5.  &nbsp;
    
    `npm start app.js`
    

## Test the nodejs app on the instance on port 3000

- e.g.. http://3.252.166.160:3000/posts

&nbsp;

**Types of monitoring**

horizontal vs vertical scaling

vertical may be preferred as it uses the same machine with more resources

<img src="../../_resources/7f8805a8f590e156108c75410409beeb.png" alt="7f8805a8f590e156108c75410409beeb.png" width="836" height="734">
