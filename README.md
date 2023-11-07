<h1>Install and Set Up Fail2Ban</h1>


<h2>Description</h2>
In this project we will install and set up Fail2Ban to help in preventing and mitigating SSH attacks since we need to leave this port open in order to access the server remotely for updates and maintenance. We will also show how to enable nginx protection since this server also uses an nginx webserver. The main focus in this project however is to to protect against SSH attacks.
<br />


<h2>Environments Used: </h2>

- <b>Ubuntu 20.04 LTS, running on a DigitalOcean Droplet connected to over SSH from a local Manjaro system</b>

<h2>Installation and Set-Up walk-through:</h2>

<p align="center">
Fail2ban is already in the Unbuntu repositories so we can install normally using apt: <br/>
<img src="https://i.imgur.com/nxzvgU2.png" height="80%" width="80%" alt="Intall Fail2ban"/>
<br />
<br />
Once the install is completed we will need to navigate to the directory with the config file:  <br/>
<img src="https://i.imgur.com/T5neE5D.png" height="80%" width="80%" alt="Navigate to config file"/>
<br />
<br />
We will check the first part of the config file to see that since this file could update and be overwritten when Fail2ban updates, we will need to create a .local config: <br/>
<img src="https://i.imgur.com/wWY1GPW.png" height="80%" width="80%" alt="Inspect config file"/>
<br />
<br />
Next, we will copy the contents of jail.conf into a jail.local file so we can create and edit our own config, then open this is nano for editing:  <br/>
<img src="https://i.imgur.com/016HywT.png" height="80%" width="80%" alt="Create and open config file"/>
<br />
<br />
We will leave some settings at their deafaults but will change the bantime to be 30 minutes:  <br/>
<img src="https://i.imgur.com/v2Wzufb.png" height="80%" width="80%" alt="Edit config file"/>
<br />
<br />
Next, we will check the default action for fail2ban when it detects an issue, default is to update iptables to block the nefarious IP from the server. Other actions, like email notifications are listed priot to this line and can be added by changing the variable in this line:  <br/>
<img src="https://i.imgur.com/FBs2I33.png" height="80%" width="80%" alt="Leave default action"/>
<br />
<br />
Then we will enable sshd monitoring by adding a line to the config file:  <br/>
<img src="https://i.imgur.com/NX34VIw.png" height="80%" width="80%" alt="Enable sshd monitoring"/>
<br />
<br />
Since updating the config and rules we will test the configuration and once successfull will then start the Suricata service:  <br/>
<img src="https://i.imgur.com/XDrkJK6.png" height="80%" width="80%" alt="Test and start Suricata"/>
<br />
<br />
We will then check the status of the service to make sure it has started and running successfully:  <br/>
<img src="https://i.imgur.com/97rtZ9A.png" height="80%" width="80%" alt="Check status of Suricata"/>
<br />
<br />
We will also check the Suricata log file to confirm that it has successfully started:  <br/>
<img src="https://i.imgur.com/iWLsXPT.png" height="80%" width="80%" alt="Check status of Suricata"/>
<br />
<br />
Next, we will want to test Suricata to make sure it is detecting malicious traffic:  <br/>
<img src="https://i.imgur.com/zf1B8tF.png" height="80%" width="80%" alt="Test Suricata"/>
<br />
<br />
We will now check Suricata's fast.log file to see if it detected the malicious test, we can see that it was successfull. Suricata is installed and running successfully!  <br/>
<img src="https://i.imgur.com/mXPec1E.png" height="80%" width="80%" alt="Test Suricata"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
