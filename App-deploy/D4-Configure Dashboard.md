**Set up dashboard**

1.  Select the instance of interest.
2.  Navigate to monitoring to view widgets.
3.  Turn on monitoring option.
4.  ![_resources/da0977d7639ebfd434b0f5ef07c7664e.png](https://github.com/vrangr-ops/App-development/blob/main/_resources/da0977d7639ebfd434b0f5ef07c7664e.png?raw=true)
)
5.  Select add to dashboard using the 3 point menu.
6.  save the widgets on dashboard.

&nbsp;

**Adding alarms**

1.  From dashboard.
    
2.  Select the navigation pane, choose **Alarms**, **All Alarms**.
    
3.  Choose **Select metric**.
    
4.  In the **All metrics** tab, choose **EC2 metrics**.
    
5.  Choose a metric category (for example, **Per-Instance Metrics**).
    
6.  ![_resources/cpuutil.png](https://github.com/vrangr-ops/App-development/blob/main/_resources/cpuutil.png)
7.  Search the instance that you want listed for **CPUUtilization**.
    
8.  Under **Conditions**, specify the following:
    
    - For **Threshold type**, choose **Static**.
        
    - For **Whenever CPUUtilization is**, specify **Greater**. Under **than...**, specify the threshold that is to trigger the alarm to go to ALARM state if the CPU utilization exceeds this percentage. For example, 70.
        
    - ![_resources/Conditions.png](https://github.com/vrangr-ops/App-development/blob/main/_resources/Conditions.png)
9.  Under **Notification**, choose **In alarm** 
    
10. Select an existing SNS topic - add your email address
11. Select send notification to email
    - ![](https://github.com/vrangr-ops/App-development/blob/main/_resources/email.png)




12\. Email notification should be sent should look like the example below

![](https://github.com/vrangr-ops/App-development/blob/main/_resources/2b49daa61b1dd0692fff2a53058e6660.png)

&nbsp;

**Overview of config for alarm and complete dashboard**

![](https://github.com/vrangr-ops/App-development/blob/main/_resources/0fd74009b06cf43d20c345c33959b18c.png) width="835" height="378" class="jop-noMdConv">

&nbsp;



&nbsp;

Further info see - https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/US_AlarmAtThresholdEC2.html
