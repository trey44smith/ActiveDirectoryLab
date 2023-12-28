<h1>Active Directory Home Lab</h1>

 ### [YouTube Demonstration]()

<h2>Description</h2>
Creating an Active Directory Home Lab using Windows 10 on VirtualBox. I then added users with PowerShell.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Active Directory</b>
- <b>PowerShell</b>

<h2>Environments Used </h2>

- <b>Windows 10</b>
- <b>Windows Server 2019</b>
- <b>VirtualBox</b>

<h2>Project Diagram:</h2>

<p align="center">
<img src="https://i.imgur.com/oweBwW5.png" height="80%" width="80%" alt="Projecte Diagram"/>
<br />
</p>

<h2>Part 1:</h2>

<p>
Step 1: Download and install VirtualBox and the Extension Pack(https://www.virtualbox.org/wiki/Downloads) <br />
Step 2: Download the Windows 10 64-bit ISO (https://www.microsoft.com/en-us/software-download/windows10ISO) and Server 2019 64-bit ISO (https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)<br />
Step 3: Create the Virtual Machine on VirtualBox with the following fields<br />
 - Name: DC<br />
 - Version: Other Windows (64-bit)<br />
 - Memory Size: 2048 mb<br />
 - File Location and Size: 20.00 GB<br />
Step 4: Update Settings<br />
- Settings > General > Advanced > Shared Clipboard: Biderectional<br />
- Settings > General > Advanced > Drag'n'Drop: Biderectional <br />
- Settings > General > Network > Adapter 2 > Enable Network Adapter > Attached to: Internal Network<br />
Step 5: Start the Virtual Machine (VM)<br />
- Select Server 2019 ISO and click start<br />
Step 6: Install Server 2019<br />
- Select Windows 2019 Standard Evaluation (Desktop Experience)<br />
- Select Custom Install<br />
- Click next until installation begins<br />
- ** Do not press any buttons while system restarts during installation **<br />
Step 7: Enter Administrator Password<br />
- Use Password1 for convenience<br />
- This is okay because this is a homelab where we will be the only one using the environment<br />
Step 8: Click Input > Keyboard > Insert Ctrl+Alt+Del to bring up the login page and login<br />
Step 9: Install VM Guest Experience<br />
- Devices > Insert Guest Additions CD Image<br />
Step 10: Click File Explorer > This PC > VirtualBox Guest Additions > Run VBoxWindowsAdditions-amd64<br />
Step 11: Click Reboot Later<br />
Step 12: Shutdown the VM<br />
Step 13: Start the VM and login to Windows<br />
</p>

<h2>Part 2:</h2>

<p>
Step 1: 
Step 2: 
Step 3: 
Step 4: 
Step 5:
Step 6: 
Step 7: 
Step 8: 
Step 9: 
Step 10: 
Step 11: 
Step 12: 
Step 13: 
</p>


<br />

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
