## Load balancer

1.  Go to EC2
2.  Navigate to load balancers in the side menu
3.  Create load balancer
4.  Load balancer types: Select Application Load Balancer
5.  Configure as below
   
7.  | Load balancer name | <span style="font-weight: 400; background-color: rgb(16, 21, 26);">Follow an appropriate convention. e.g. organization-name-project title-lb.</span> |
    | --- | --- |
    | Scheme | Internet-facing |
    | Availability zones and subnets | Select zones in Ireland |
    | Load balancer IP address type | IPv4 |
    | Security groups | Select security group e.g. se-name-app-sg|
    | Target group | Create target group  <br><br/>e.g. se-name-app-tg |
    | Load balancer tags - *optional* | Give the balancer a searchable tag |
    

Then select create load balancer

## Autoscaling group template

*Using a template*

1.  Create launch template
2.  *Configure with the options selected below.*
3.  <div class="joplin-table-wrapper"><table border="1" style="border-collapse: collapse; width: 100.008%; height: 195.767px;" class="jop-noMdConv"><colgroup class="jop-noMdConv"><col style="width: 49.9587%;" class="jop-noMdConv"><col style="width: 49.9587%;" class="jop-noMdConv"></colgroup><thead class="jop-noMdConv"><tr class="jop-noMdConv" style="height: 36.7472px;"><th scope="col" class="jop-noMdConv" style="height: 36.7472px;"><p><span class="jop-noMdConv" style="color: rgb(255, 255, 255);"><span style="font-weight: bolder;" class="">Name</span></span></p><ul style="font-weight: 400;" class="jop-noMdConv"></ul></th><th scope="col" class="jop-noMdConv" style="height: 36.7472px;"><span style="font-weight: 400; background-color: rgb(16, 21, 26);" class="">Follow an appropriate convention. e.g. organization-name-project title-tg.</span></th></tr></thead><tbody class="jop-noMdConv"><tr class="jop-noMdConv" style="height: 54.0057px;"><td class="jop-noMdConv" style="height: 54.0057px;"><span style="font-weight: bold;" class="">Application and OS Images</span></td><td class="jop-noMdConv" style="height: 54.0057px;"><p>Select image template (ami)</p><p>e.g.se-luke-nodejs20-app-image</p></td></tr><tr class="jop-noMdConv" style="height: 27.0028px;"><td class="jop-noMdConv" style="height: 27.0028px;"><span style="font-weight: bolder; background-color: rgb(16, 21, 26);" class="">Instance type</span></td><td class="jop-noMdConv" style="height: 27.0028px;"><p>t3 micro</p></td></tr><tr class="jop-noMdConv" style="height: 24.0057px;"><td class="jop-noMdConv" style="height: 24.0057px;"><span style="font-weight: bolder;" class="">Key pair</span></td><td class="jop-noMdConv" style="height: 24.0057px;">Select your SSH key</td></tr><tr class="jop-noMdConv" style="height: 54.0057px;"><td class="jop-noMdConv" style="height: 54.0057px;"><span style="font-weight: bolder;" class="">Network setting</span></td><td class="jop-noMdConv" style="height: 54.0057px;"><p>Select existing group.</p><p>Select se-name-nodejs20-sg</p></td></tr></tbody></table></div>

4\. Select save

5\. Adding tags
- ![](https://github.com/vrangr-ops/App-development/blob/main/_resources/manage%20tags.png)


- Give the group a key tag which can be searchable.

&nbsp;

## Set up Auto-Scalling Group:

1.  EC2
2.  Navigate to autoscaling group from side menu.
3.  create auto scaling group
4.  <div class="joplin-table-wrapper"><table border="1" style="border-collapse: collapse; width: 100.008%; height: 195.767px;" class="jop-noMdConv"><colgroup class="jop-noMdConv"><col style="width: 49.9587%;" class="jop-noMdConv"><col style="width: 49.9587%;" class="jop-noMdConv"></colgroup><thead class="jop-noMdConv"><tr class="jop-noMdConv" style="height: 36.7472px;"><th scope="col" class="jop-noMdConv" style="height: 36.7472px;"><p><span class="jop-noMdConv" style="color: rgb(255, 255, 255);"><span style="font-weight: bolder;" class="">Name</span></span></p><ul style="font-weight: 400;" class="jop-noMdConv"></ul></th><th scope="col" class="jop-noMdConv" style="height: 36.7472px;"><span style="font-weight: 400; background-color: rgb(16, 21, 26);" class="">Follow an appropriate convention. e.g. organization-name-project title-asg.</span></th></tr></thead><tbody class="jop-noMdConv"><tr class="jop-noMdConv" style="height: 54.0057px;"><td class="jop-noMdConv" style="height: 54.0057px;"><span style="font-weight: bold;" class="">Launch template</span></td><td class="jop-noMdConv" style="height: 54.0057px;"><p>Select image template (ami)</p><p>e.g.se-burhan-nodejs20-app-asg</p></td></tr><tr class="jop-noMdConv" style="height: 27.0028px;"><td class="jop-noMdConv" style="height: 27.0028px;"><span style="background-color: rgb(16, 21, 26);" class=""><b class="jop-noMdConv">Availability zones</b></span></td><td class="jop-noMdConv" style="height: 27.0028px;"><p>Select zones in Europe/Ireland</p></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="background-color: rgb(16, 21, 26);" class=""><b class="jop-noMdConv">Integrate with other services</b></span></td><td class="jop-noMdConv"><p>Attach a new load balancer</p><ul class="jop-noMdConv"><li class="jop-noMdConv">App load balancer</li><li class="jop-noMdConv">Internet facing</li></ul></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="background-color: rgb(16, 21, 26);" class=""><b class="jop-noMdConv">Target group</b></span></td><td class="jop-noMdConv"><p>Create new target group</p><ul class="jop-noMdConv"><li class="jop-noMdConv">se-burhan-nodejs20-app-asg</li></ul></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="background-color: rgb(16, 21, 26);" class=""><b class="jop-noMdConv">VPC lattice</b></span></td><td class="jop-noMdConv"><p>No VPC lattice</p></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="background-color: rgb(16, 21, 26);" class=""><b class="jop-noMdConv">Health checks</b></span></td><td class="jop-noMdConv"><p>Turn on elastic load balance health checks</p></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="background-color: rgb(16, 21, 26);" class=""><b class="jop-noMdConv">Group size</b></span></td><td class="jop-noMdConv"><p>capacity - 2</p></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="background-color: rgb(16, 21, 26);" class=""><b class="jop-noMdConv">Scaling</b></span></td><td class="jop-noMdConv"><p>min-2</p><p>max-3</p></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="background-color: rgb(16, 21, 26);" class=""><b class="jop-noMdConv">Automatic scaling</b></span></td><td class="jop-noMdConv"><p>target tracking scaling policy</p></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="background-color: rgb(16, 21, 26);" class=""><b class="jop-noMdConv">instance maintenance policy</b></span></td><td class="jop-noMdConv"><p>No policy</p></td></tr><tr class="jop-noMdConv"><td class="jop-noMdConv"><span style="background-color: rgb(16, 21, 26);" class=""><b class="jop-noMdConv">Additional capacity</b></span></td><td class="jop-noMdConv"><p>default</p></td></tr></tbody></table></div>

5\. Select next from additional settings

![](https://github.com/vrangr-ops/App-development/blob/main/_resources/Additional%20setting.png)

6\. Select next

![](https://github.com/vrangr-ops/App-development/blob/main/_resources/fea0d2249de340ffbe4913bf28575f95.png)

7\. Add tags - give a tag that can be easily searched

![](https://github.com/vrangr-ops/App-development/blob/main/_resources/eb16c5633886bb806de7ec5cf8be3187.png)

8\. To check its running correctly:

![](https://github.com/vrangr-ops/App-development/blob/main/_resources/743b0ef41d74aa4c64ab7f18ceaf2582.png)

9\. To see if the Nodejs app is working and the app is polulated using the database, navigate using a web browser to the address below.
HTTP://IP_ADD/posts
