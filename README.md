<h1>Active Directory Home Lab</h1>

 ### [YouTube Demonstration](https://youtu.be/uEu56wcAjVk)

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

<h2>Part 1: Create the Domain Controller Virtual Machine</h2>

<p>
Step 1: Download and install VirtualBox and the Extension Pack(https://www.virtualbox.org/wiki/Downloads) <br />
 <br />
Step 2: Download the Windows 10 64-bit ISO (https://www.microsoft.com/en-us/software-download/windows10ISO) and Server 2019 64-bit ISO (https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)<br />
 <br />
Step 3: Create the Virtual Machine on VirtualBox with the following fields<br />
 - Name: DC<br />
 - Version: Other Windows (64-bit)<br />
 - Memory Size: 2048 mb<br />
 - File Location and Size: 20.00 GB<br />
 <br />
Step 4: Update Settings<br />
- Settings > General > Advanced > Shared Clipboard: Biderectional<br />
- Settings > General > Advanced > Drag'n'Drop: Biderectional <br />
- Settings > General > Network > Adapter 2 > Enable Network Adapter > Attached to: Internal Network<br />
 <br />
Step 5: Start the Virtual Machine (VM)<br />
- Select Server 2019 ISO and click start<br />
 <br />
Step 6: Install Server 2019<br />
- Select Windows 2019 Standard Evaluation (Desktop Experience)<br />
- Select Custom Install<br />
- Click next until installation begins<br />
- ** Do not press any buttons while system restarts during installation **<br />
 <br />
Step 7: Enter Administrator Password<br />
- Use Password1 for convenience<br />
- This is okay because this is a homelab where we will be the only one using the environment<br />
 <br />
Step 8: Click Input > Keyboard > Insert Ctrl+Alt+Del to bring up the login page and login<br />
 <br />
Step 9: Install VM Guest Experience<br />
- Devices > Insert Guest Additions CD Image<br />
 <br />
Step 10: Click File Explorer > This PC > VirtualBox Guest Additions > Run VBoxWindowsAdditions-amd64<br />
 <br />
Step 11: Click Reboot Later<br />
 <br />
Step 12: Shutdown the VM<br />
 <br />
Step 13: Start the VM and login to Windows<br />
</p>

<h2>Part 2: Set Up IP Addressing</h2>

<p>
Step 1: Navigate to Network & Internet Settings <br />
- Click Ethernet > Change adapter options <br />
<br />
Step 2: Right click one of the ethernets and select Status > Details <br />
- Look at the IPv4 address. If it shows 10. something, then it is the ethernet connected to the internet <br />
<br />
Step 3: Right click the same ethernet chosen previously. Select Rename. <br />
- Rename it "_INTERNET_" <br />
<br /> 
Step 4: Right click the other ethernet. Select Rename. <br />
- Rename it "X_Internal_X" <br />
<br /> 
Step 5:Right Click on "X_Internal_X". Select Properties. <br />
- Double-Click: "Internet Protocol Version 4 (TCP/IPv4)" <br />
- Click: "Use the following IP address:" <br />
<br />
Step 6: Enter the following and click "Ok": <br />
- IP address: 172.16.0.1 <br />
- Subnet mask: 255.255.255.0 <br />
- * LEAVE DEFAULT GATEWAY BLANK, DC WILL SERVE AS THIS * <br />
- Preferred DNS server: 172.16.0.1 <br />
</p>

<h2>Part 3: Rename the PC and Install Active Directory Domain Services</h2>

<p>
Step 1: Right click the start menu. Navigate to System. <br />
- Click "Rename this PC" <br />
- Name the PC, "DC" <br />
- Click Restart. <br />
<br />
Step 2: Login to the machine. <br />
<br />
Step 3: Click "Add Roles and Features" <br />
- Click Next until you reach "Server Selection" <br /> 
- Make sure that "DC" is selected and click Next <br /> 
- Choose "Active Directory Domain Services" <br /> 
- Click Next until the Install button appears and install the role. <br />
<br /> 
Step 4: Click the flag with the yellow symbol in the upper left corner <br /> 
- Click the link that says " Promotethe server to a domain controller" <br /> 
<br /> 
Step 5: Click "Add a new forest" <br /> 
- Enter "mydomain.com" in the Root domain name section <br /> 
- Click Next, make the password "Password1" <br /> 
- Click Next until you are prompted to install. <br /> 
- The system will automatically restart. <br /> 
<br />
Step 6: Login to the system. <br /> 
</p>

<h2>Part 4: Create Domain Admin account and </h2>

<p>
Step 1: Navigate to Start > Windows Administrative Tools > Active Directory Users and Computers <br /> 
- Click mydomain.com <br /> 
<br />
Step 2: Right Click on mydomain.com > New > Organizational Unit <br /> 
- Enter "_ADMINS" in the Name section <br /> 
- Uncheck the checked box and click ok <br /> 
<br />
Step 3: Right Click on mydomain.com > New > User <br /> 
- Enter your First and Last name <br /> 
- User logon name will follow this convention: "a-'FIRST INITIAL''LAST NAME'" <br /> 
&nbsp; - i.e. a-tsmith <br /> 
- Click Next and use "Password1" as the password <br /> 
- Uncheck "User must change password at next logon" and check "Password never expires" <br /> 
- Click next and finish. <br /> 
<br /> 
Step 4: Navigate to mydomain.com > _ADMINS <br /> 
- Right click on the newly created user <br /> 
- Navigate to Properties > Member Of <br /> 
- Click Add <br /> 
- Enter "domain admins" in the "Enter the object names to select" box and click Check Names <br /> 
- Click Ok, Apply, Ok <br /> 
<br /> 
Step 5: Sign Out of the machine. <br /> 
<br />
Step 6: Select Other user on the login screen. <br /> 
- Use the newly created user's credentials.  <br /> 
</p>

<h2>Part 5: Install RAS/NAT and configure DHCP Server</h2>

<p>
Step 1: Click "Add Roles and Features" <br />
- Click Next until you reach "Server Selection" <br /> 
- Make sure that "DC" is selected and click Next <br /> 
- Choose "Remote Access" <br /> 
- Click Next until you reach "Role Services" <br /> 
- Check "Routing" <br /> 
- Click Next until the Install button appears and install the role. <br />
<br />
Step 2: In the upper right hand corner, navigate to Tools > Routing and Remote Access
<br />
 <br />
Step 3: Right click on DC in the menu <br />
- Select "Configure and enable" <br />
- Click Next and select the option that says "Network address translation (NAT)" <br />
- * Please close and repeat step 2 and 3 if the network interfaces section is empty when you click next * <br />
- Select the "Use this public interface to connect to the internet" option <br />
- Select the "_INTERNET_" option and click next and finish <br />
<br /> 
Step 4: Step 1: Click "Add Roles and Features" <br />
- Click Next until you reach "Server Selection" <br /> 
- Make sure that "DC.mydomain.com" is selected and click Next <br /> 
- Choose "DHCP Server" <br /> 
- Click Next until the Install button appears and install the role. <br />
<br /> 
Step 5: In the upper right hand corner, navigate to Tools > DHCP <br /> 
<br />
Step 6: Right Click IPv4, select "New Scope", and click Next <br /> 
- Enter 172.16.0.100-200 in the name section, click next <br /> 
- Enter 172.16.0.100 in the Start IP address <br /> 
- Enter 172.16.0.200 in the End IP address <br /> 
- Change the length to 24 <br /> 
- Keep the Subnet mask as 255.255.255.0 <br /> 
- Click next twice and then enter 8 days, or your preference, for lease duration <br /> 
- Click next twice and then enter 172.16.0.1 as the Router IP address <br /> 
- Make sure to click add and then Next <br /> 
- Click Next until you press finish <br /> 
<br /> 
Step 7: Right click dc.mydomain.com and select authorize <br /> 
<br /> 
Step 8: Right click dc.mydomain.com and select refresh <br /> 
<br /> 
</p>


<h2>Part 6: Add users using PowerShell</h2>

<p>
Step 1: Download the .ps1 and the .txt file from windows in the virtual machine <br />
- Save in a location that you won't forget <br />
<br />
Step 2: Open the text file, add your name on the first line, and save the file <br />
<br />
Step 3: Click the start button and navigate to Windows Powershell <br />
- Right click and Run as administrator <br />
- Click yes <br />
<br /> 
Step 4: Click open and select the .ps1 file <br />
<br /> 
Step 5: In the command window enter: Set-ExecutionPolicy Unrestricted <br />
- Click "yes to all" <br />
<br />
Step 6: CD to the location of the text file <br />
- run ls to ensure the text file is there in the directory <br />
<br /> 
Step 7: Run the .ps1 file, and click run when the message window appears <br />
<br /> 
Step 8: Navigate to Active Directory Users and Computers <br />
- Right click on mydomain.com and select Refresh <br />
- Users folder will now be created and created users will be found <br />
<br /> 
Step 9: Right click mydomain.com and select find <br />
- This allows you to search for any created user <br />
<br />
</p>

<h2>Part 7: Create Windows 10 Virtual Machine</h2>

<p>
Step 1: Go to VirtualBox <br />
- Select New <br />
- Name the machine "Client1" <br />
- Select Windows 10 64-bit as the Version <br />
- Click continue <br />
- Stick with 2048 MB RAM unless you know your system can handle more <br />
- Click continue until the machine is created <br />
<br />
Step 2: Update Settings<br />
- Settings > General > Advanced > Shared Clipboard: Biderectional <br />
- Settings > General > Advanced > Drag'n'Drop: Biderectional <br />
- Settings > General > Network > Adapter 1 > Enable Network Adapter > Attached to: Internal Network <br />
<br />
Step 3: Start the machine <br />
<br /> 
Step 4: Start the Virtual Machine (VM) <br />
- Select Windows 10 ISO, click choose, and click start <br />
<br /> 
Step 5: Click Next and Install once the machine restarts <br />
- Click "I don't have a product key" <br />
- Select Windows 10 Pro and click next until you reach Windows Setup <br />
- Select Custom and next <br />
- The system will restart multiple times during installation <br />
- ** Do not press any buttons while system restarts during installation **<br />
<br />
Step 6: Choose your language and keyboard layout <br />
<br /> 
Step 7: Choose continue with limited setup <br />
<br /> 
Step 8: Name the PC "user" and click next twice <br />
<br /> 
Step 9: Disable all options in the privacy settings window <br />
<br /> 
Step 10: Click not now for Cortana <br />
<br /> 
Step 11: Run command line and run the ipconfig command to ensure the internet is configured properly <br />
- Next, run "ping google.com" <br />
<br /> 
Step 12: Right click start menu and navigate to System <br />
- Scroll down and click "Rename this PC (advanced)" <br />
- Click Change <br />
- Enter "Client1" in the Computer name section <br />
- In the Member of section, enter mydomain.com in the Domain box <br />
<br />  
Step 13: Enter your account credentials when prompted, click ok, and click restart <br />
<br />
Step 14: Navigate to the login screen and select Other user <br />
<br />
Step 15: Login with any user account credentials <br />
<br />
Step 16: Successful login means the home lab has been set up! <br />
<br />
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
