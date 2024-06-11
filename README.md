<h1>Azure Cloud Detection Lab</h1>

This lab was created over at [Cyberwox Academy](https://cyberwoxacademy.com/azure-cloud-detection-lab-project/). Thanks for putting together this lab!

<h2>Learning Objectives:</h2>

- Configuration & Deployment of Microsoft Azure virtual machines, Log Analytics Workspaces, and Microsoft Sentinel
- Implement network and virtual machine security best practices (Just-In-Time (JIT) Protocol)
- Utilize Data Connectors to use with Microsoft Sentinel, a cloud-native SIEM (Security Information and Event Management) for analysis
- Understanding Windows Security Event logs
- Using Kusto Query Language (KQL) to query logs
- Write custome analytic rules to detect Microsoft Security Events
- Utilze MITRE ATT&CK to map adversary tactics, techniques, and procedures (TTPs)

<h2>Tools</h2>

<b>The lab is completely cloud-based all done within Microsoft Azure</b>
- Microsoft Azure
- Remote Desktop Protocol

<h2>Overview</h2>

![](images/topology.jpg)

<b>MITRE ATT&CK</b>

![](images/Mitre.jpg)

In this lab I obeserved the [Mitre att&ack Persistence](https://attack.mitre.org/tactics/TA0003/).</br>Since a schedule taks/job is a technique used that can allow malicious actors in an environment.

<h2>Steps</h2>
  
### Creating a Microsoft Azure account
> Using my new Azure account to use the $200 credit for 30 days that I have remaining. </br> creating a new azure resource group for this lab

![](images/photo1.jpg)

### Creating and delopying a VM
> With this VM were going to enable a security freature called [Just-In-Time (JIT) access](https://learn.microsoft.com/en-us/azure/defender-for-cloud/just-in-time-access-usage?tabs=jit-config-asc%2Cjit-request-asc). 

![](images/photo3.jpg)

![](images/photo5.jpg)

In the network security group (nsg) for my resource you can see JIT Rule is enable with allow only for my IP (which is blanked out) and below is deny everything else
![](images/photo6.jpg)

### Setting up Log Analytics Workspace & deploying Microsoft Sentinel

![](images/photo7.jpg)

![](images/photo8.jpg)

### Enabling Windows Security Events within the Data Connectors tab
> I enabled this because it allows me to stream all security events from the windows machine into Sentinel

![](images/photo9.jpg)

![](images/photo10.jpg)

### Logging into the VM
> Checking security events and testing them in the logs in Sentinel to make sure everything is working

![](images/photo11.jpg)

![](images/photo12.jpg)

### Adding a security policy for the security event to monitor
>Afterwards creating a task schedule event trigger called Malicious Task that would trigger a browser to start. </br> I did this to generate the EventID 4698 so it can show in the event viewer

![](images/photo15.jpg)

![](images/photo16.jpg)

![](images/photo17.jpg)

![](images/photo18.jpg)

![](images/photo19.jpg)

### Creating KQL query
>searching for the eventid 4698 that was previously triggered within Sentinel Logs. Also parsing information such as the user, task, process id and host in a KQL query

![](images/photo20.jpg)

### Creating an Alaytics Rule with the KQL Query
>This rule will trigger a log to generate whenever the alert occurs.
></br>This trigger will happens every 5 mins

![](images/photo21.jpg)

![](images/photo22.jpg)

![](images/photo23.jpg)

![](images/photo24.jpg)

### Testing out the trigger to to make sure it works
>The VM opened a the Edge browser after I scheduled an event to occur
></br>Since the log generates every 5 mins I had to wait to see if anything occured

![](images/photo25.jpg)

![](images/photo26.jpg)

![](images/photo27.jpg)

### Checking out the details
> Closing the ticket after assigning it to me with a reason being a FalsePostive

![](images/photo29.jpg)
