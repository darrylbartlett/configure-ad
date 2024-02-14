<p align="center">
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/0ef3d6a9-abb7-490b-aab1-b19002987fd4"/>
</p>

<h1>Active Directory (On-premise) Setup</h1>
This tutorial outlines the setup of on-premise Active Directory, connecting to a client computer, and managing different containers and user accounts.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure for creating Virtual Machines
- Active Directory (On-premise)

<h2>Operating System Used</h2>

- Windows Server 2022 for a domain controller
- Windows 10 Pro (22H2) for a client computer

<h2>List of Prerequisites</h2>

- Creation of an Azure Virtual Machine (VM) with Windows 10 Pro as a client computer
- Creation of an Azure Virtual Machine (VM) with Windows Server 2022 as a domain controller
    - This domain controller has been setup with a static IP on its virtual network interface card
- Connecting to the VMs using Remote Desktop Connection with their created public IPs, usernames and passwords
<br />

<h2>Setup a Connection Between the Client and Domain Controller</h2>

<p>Using Remote Desktop Connection, log into the Client virtual machine.</p>
<p>'Ping -t' the domain controller VM from the Command Line. Use its private IP.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/c595fc7d-d1f6-431e-a955-d2c83c9b3895"/>
</p>
<br />

<p>Log into the domain controller VM.</p>
<p>From the Start Menu, open 'Windows Defender Firewall with Advanced Security'.</p>
<p>On the left panel, select Inbound Rules.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/c2e1c22a-3092-4ee8-9a96-7111c382f39b"/>
</p>
<br />

<p>In the middle panel where the Inbound Rules are displayed, click on Protocol to sort by this column.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/c822edc5-b083-4ed9-891f-b412912c3fe7"/>
</p>
<br />

<p>Under the Protocol column, find the rows with ICMPv4.</p>
<p>Select the two rows called 'Core Networking Diagnostics – ICMP Echo Request (ICMPv4-In)'.</p>
<p>Right-click on one of the highlighted rows and select Enable Rule from the sub-menu.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/e28a309d-ed58-4789-ba1e-8c3fe534796a"/>
</p>
<br />

<p>Both rows should be showing a green check mark beside them.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/489725e3-ad11-4d32-af17-1f55634a7d78"/>
</p>
<br />

<p>Go back to the Client VM and see if the ping shows connection.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/3680108d-e563-4406-a983-4b48fcd19a07"/>
</p>
<br />

<h2>Install Active Directory</h2>

<p>Go back to the domain controller VM and open Server Manager <i>(it may already be open by default).</i></p>
<p>At the top right-hand corner, click on the Manage menu.</p>
<p>Select Add Roles and Features.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/8c6fc435-cb9e-4090-bc5b-4c4a98be964d"/>
</p>
<br />

<p>The Add Roles and Features Wizard will open.</p>
<p>Keep the default prompts until you get to the Server Roles screen.</p>
<p>Select the checkbox beside Active Directory Domain Services. A pop-up window is displayed. Click the Add Features button.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/aab1a9a7-d977-410d-8d6f-7b1f59e07cb0"/>
</p>
<br />

<p>Active Directory Domain Services is now checked.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/4cc15990-d468-489d-b3c9-b28908dc069a"/>
</p>
<br />

<p>Click Next.</p>
<p>Follow the rest of the default prompts. Click Install at the Confirmation screen. The install may take a few minutes.</p> 
<p>Click the Close button when the install is finished.</p>
<p>At the top right-hand corner of the Server Manager screen, a yellow triangle with an exclamation mark is displayed.</p>
<p>Click the yellow triangle and select ‘Promote this server to a domain controller’.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/d2c4135d-b0ce-4722-94b5-2aee34fda1a7"/>
</p>
<br />

<p>The Active Directory Domain Services Configuration Wizard window will open.</p>
<p>On the Deployment Configuration screen, select ‘Add a new forest’. Enter the domain name to be used.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/8c29d142-e52a-4b74-94d0-09d6a25e4f4d"/>
</p>
<br />

<p>Click Next.</p>
<p>On the Domain Controller Options screen, enter a password. This can be anything…it won’t be used anywhere.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/2cfcd541-cfbf-44ae-b712-1dcbba705e15"/>
</p>
<br />

<p>Click Next and keep the default prompts for everything else.</p>
<p>Click Install at the Prerequisites Check screen. This may take a few minutes to complete.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/7c710606-54dd-4c09-8dda-3990269464cc"/>
</p>
<br />

<p>The remote session will restart after the install is done.</p>
<p>Log back in using the new domain name you created with your local admin username and password.</p>
<p><i>Ex. Username should be entered like this: dbdomain.com\username</i></p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/7c710606-54dd-4c09-8dda-3990269464cc"/>
</p>
<br />

<h2>Create Organizational Units and An Admin User Account</h2>

<p>Open Server Manager.</p>
<p>At the top right-hand corner, select the Tools menu and click Active Directory Users and Computers (this can also be found through the Start Menu).</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/41f6f968-3e77-446d-9e4c-62d5b5a9940a"/>
</p>
<br />

<p>Create Organizational Units for:</p>

- _EMPLOYEES
- _ADMINS

<p>To do this, right-click on the domain name on the left side of the screen. Select New on the sub-menu and then select Organizational Unit.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/6a84d6d3-43f2-4dff-84cc-0fcb9e39faad"/>
</p>
<br />



<p>To do this, right-click on the domain name on the left side of the screen. Select New on the sub-menu and then select Organizational Unit.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/6a84d6d3-43f2-4dff-84cc-0fcb9e39faad"/>
</p>
<br />



