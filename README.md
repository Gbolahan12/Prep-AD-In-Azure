
<p align="center">
<img src="https://camo.githubusercontent.com/dfe5ae7df64e6027d15e69ec66b2fd9856adff5b35885f5fd3cf53fe75bd80d1/68747470733a2f2f6d656469612e6c6963646e2e636f6d2f646d732f696d6167652f76322f443444313241514650494d54326e6c546264412f61727469636c652d636f7665725f696d6167652d736872696e6b5f3732305f313238302f61727469636c652d636f7665725f696d6167652d736872696e6b5f3732305f313238302f302f313639303530323539353139313f653d3231343734383336343726763d6265746126743d7948373835696c506d6670715667634b6b4733366b70686b50526777615a5052572d53385f4d3975666473" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />

<h1>Setting Up Active Directory Infrastructure in Azure</h1>


<h2>Description</h2>
In this project I create two VMs (Virtual Machines), one running Windows Server, to act as a Domain Controller. The other VM will act as a client, running Windows 10 that will join the domain. In later projects I will deploy AD, run a script that will create users in the domain, which I can log into from the client VM, then manage the accounts and update the group policies, all to simulate a real life IT environment!  <br/>
<br />


<h2>Environments and Utilities Used</h2>

- <b>Microsoft Azure</b>
- <b>Virtual Machines</b>
- <b>Remote Desktop Connection</b>


<h2>Operating Systems Used </h2>

- <b>Windows Server </b>
- <b>Windows 10</b>

<h2>Project Walk-through:</h2>

<p align="center">
Navigate to Microsoft Azure and create a resource group: <br/>
<img src="https://i.imgur.com/qSCFXWH.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Next, create a virtual network like so: <br/>
<img src="https://i.imgur.com/ilI3tGJ.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Once my resource group and network is created, I'll create and set up the virtual machine that will act as our Domain Controller. For the image, make sure you use Windows Server:  <br/>
<img src="https://i.imgur.com/2LoNsRy.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
In the Networking tab of this VM, I'll make sure it will create itself on the virtual network I just created. I'll leave all other settings default and create this VM: <br/>
<img src="https://i.imgur.com/hYXr6eb.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Now, I'll create another VM that will serve as the client. The image for this machine should be Windows 10, NOT Windows Server like I did for the previous machine:  <br/>
<img src="https://i.imgur.com/onn13zs.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
In the Networking tab of this VM, I'll make sure it will create itself on the same virtual network of the previous machine created. I'll leave all other settings default and create this VM:  <br/>
<img src="https://i.imgur.com/MWusAfc.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
I now need to set our DC (Domain Controller) private IP address to "static" as by default it is set to "dynamic". I want this to be static, because this DC will double as a DNS (Domain Name System) server, which I will tell our client to use as a DNS server later. If the IP allocation setting were set to dynamic, the IP address could change leaving the DNS configuration of our client invalid. So, I'll go to the network settings of the DC and switch the IP allocation to static:  <br/>
<img src="https://i.imgur.com/tYmCSYH.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Next, I'll use Remote Desktop Connection to connect to the DC using its public IP and the log in credentials I created when setting up this machine:  <br/>
<img src="https://i.imgur.com/cqQEaNd.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Next, I'm going to disable the firewall (you probably wouldn't do this in real lfe, but for the sake of this lab where nothing is at stake, I'll go ahead and do it). So, to disable the firewall I'll right click on the "Start" button and select "Run". Then type "wf.msc":  <br/>
<img src="https://i.imgur.com/vgBNgDE.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Next, I need configure our clients DNS settings to the DC. To start, back in Azure, I'll grab the DCs private IP address:  <br/>
<img src="https://i.imgur.com/hIcCKZ5.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Then, I'll go to the network setting of the client machine. click on the NIC (Network Interface Card), go to settings, then DNS servers and switch from "Inherit from virtual network" to "Custom". Input the DCs private IP here and save:  <br/>
<img src="https://i.imgur.com/RbCg6wb.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
After that's saved, I'll restart the client machine:  <br/>
<img src="https://i.imgur.com/w7LjzAD.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Once the machine as restarted, I'll use Remote Desktop connection to connect to the client machine using its public IP and the log in credentials I created while setting up this machine:  <br/>
<img src="https://i.imgur.com/Sc0hZGt.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Now that I'm logged in, I will open Powershell and attempt to ping the DC using the ping command and its private IP address. In my case it'll look like this. (If there is an error and the connection timed out, double check in Azure to make sure both of the machines are on the same virtual network. If they aren't this is likely causing the error and you'll need to set up the machine again on the same network):  <br/>
<img src="https://i.imgur.com/8e2Pare.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
While I'm here I can double check that the DNS server settings are pointing to the DC. I'll run "ipconfig /all" and look for the "DNS Servers" and it should point to our DC if everything is set up properly:  <br/>
<img src="https://i.imgur.com/dmKkgz8.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />

<h2>Active Directory Infrastructure is Now Prepared! </h2>

<b>We've successfully created two VMs (Virtual Machines), one running Windows Server, to act as a Domain Controller. The other VM as a client, running Windows 10. Don't forget: In later projects I will deploy AD, run a script that will create users in the domain, which I can log into from the client VM, then manage the accounts and update the group policies, all to simulate a real life environment!  </b>
<br />
<br />
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
