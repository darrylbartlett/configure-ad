<p align="center">
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/0ef3d6a9-abb7-490b-aab1-b19002987fd4"/>
</p>

<h1>Active Directory (On-premise) Setup</h1>
This tutorial outlines the setup of on-premise Active Directory, managing different containers and user accounts, and connecting to a client computer .<br />


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

<p>Enter the name of the Organizational Unit.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/d52e0922-9a35-4d68-9e6a-938c016453d8"/>
</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/330234c6-8685-41e9-b1a9-7d37b4a98c4c"/>
</p>
<br />

<p>Create a new employee named Jane Doe. Her username will be jane_admin.</p>
<p>To do this, right-click on the domain name. Select New on the menu and then choose User.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/e7ab51d5-fdb2-480b-972e-6c72c459390e"/>
</p>
<br />

<p>Fill out the information for Jane Doe and then click Next.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/8fa42b6e-9864-447d-9c83-ea4d916c5c68"/>
</p>
<br />

<p>Enter a password for the user. Uncheck the box beside ‘User must change password at next logon’.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/71605182-0d21-4f7e-a441-264446b8b4f4"/>
</p>
<br />

<p>Click Next and then click Finish.</p>
<p>Jane Doe will show on the right side of the screen. Drag her name into the _ADMINS organizational unit. You’ll be asked if you want to move this object. Click Yes.</p>
<p>Select _ADMINS on the left side. Jane Doe should be available inside _ADMINS.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/a50b23c7-6f20-4aec-8d06-bcad8673ed6a"/>
</p>
<br />

<p>Since Jane is an admin, we’ll add her to the Domain Admins security group.</p>
<p>Right-click on Jane Doe. Select Properties on the menu.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/20c87a6b-77fc-4e16-bea0-1a8ee6556a77"/>
</p>
<br />

<p>In the Properties window, click on the Member Of tab. Click the Add button.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/f467e780-e45f-479d-8b72-13dd9ccdf220"/>
</p>
<br />

<p>Type ‘domain admins’ in the text box. Click on the Check Names button.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/3b49a471-c5ac-434a-9b86-db002a827045"/>
</p>
<br />

<p>Click OK.</p>
<p>Jane Doe is a part of the Domain Admins group. Click Apply and then click OK.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/22e68395-214e-4f6a-8928-c58e6ef4600d"/>
</p>
<br />

<p>Now logout/close your remote desktop session and log back in as jane_admin.</p>

- jane_admin can be used as the new admin account

<br />

<h2>Connect the Client to the Domain</h2>

<p>The domain controllers private IP address can be setup under the Client VM’s DNS settings in Azure. This is the domain controller’s IP that was changed to be static as part of the prerequisites. The Client needs to be restarted in Azure after the DNS has been updated.</p>

<p>Log back into the Client VM after the DNS changes are finished.</p>
<p>Go to the Start Menu and open the Settings window. On the Settings screen, select About from the bottom of the left menu.</p>
<p>On the right-side of the screen under the ‘Related settings’ options, select ‘Advanced system settings’.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/145df1ce-4e6a-4084-87a6-1379b792c435"/>
</p>
<br />

<p>The System Properties window will open. Select the Computer Name tab. Click on the Change button.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/8de2ee58-d71e-4101-bed2-aade12de7ddf"/>
</p>
<br />

<p>The Computer Name/Domain Changes window will open. Now we can connect to the new domain.</p>
<p>Under ‘Member of’, click the option button for Domain. Type in your domain name and click OK.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/7eccc5ea-dd2a-4d12-a3f3-06e0fa89db2b"/>
</p>
<br />

<p>If everything is setup okay, you should get prompted to enter a username and password. Enter the username and password for jane_admin. Remember to use the domain name as part of the username.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/21263ed4-24fa-43a6-9d60-5d3478c59ef2"/>
</p>
<br />

<p>Click OK. You should be welcomed to the domain.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/44d9fd37-916a-41da-9956-ecc2ed5ee3c5"/>
</p>
<br />

<p>Click OK. You will be prompted to restart the computer. Click OK.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/2cc9ff4a-9f11-4608-99ee-a635f05c57c2"/>
</p>
<br />

<p>Click Close on the System Properties window.</p>
<p>Click the Restart Now button.</p>
<br />

<p>Go back to the domain controller.</p>
<p>From the Start Menu, open Active Directory Users and Computers.</p>
<p>Select the Computers container on the left of the screen. The Client computer should be there.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/540c0c7c-681d-4254-9c0c-c6adc577edf0"/>
</p>

<p>Create another Organizational Unit called _CLIENTS. Click and drag the Client computer into _CLIENTS.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/60d7a542-4409-44f5-ae26-5767e327337e"/>
</p>

<h2>Setup Access to Remote Desktop for All Non-admin Users Using the Client</h2>

<p>Log back into the Client VM using jane_admin.</p>
<p>Open the Settings screen. On the right-side of the screen, under ‘Related settings’, click ‘Remote desktop’.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/26db4916-9447-4947-b97d-526c6e250103"/>
</p>

<p>At the bottom of the Remote Desktop screen, click on ‘Select users that can remotely access this PC’.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/6f9d1a15-968b-4ca3-a9da-76abf5fbfa4e"/>
</p>

<p>On the Remote Desktop Users window, click the Add button.</p>
<p>Type ‘domain users’ into the text box, and select Check Names.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/0c0361f7-3b06-4459-9c38-844e0e95044a"/>
</p>

<p>Click OK.</p>
<p>All non-admin users can login using remote desktop from the Client computer. Click OK.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/eee90fc5-18d6-4680-81bc-0fa8c066bf40"/>
</p>

<h2>Create a Non-admin User Account</h2>

<p>Go back to the domain controller computer.</p>
<p>Create another user named John Doe (username: john_user). This will be a non-admin account.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/986918fd-e682-4af6-b2e7-756ec26fbfa4"/>
</p>

<p>Create a password and uncheck the option to change the password at logon.</p>
<p>Click and drag John Doe into _EMPLOYEES.</p>
<p>
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/5778086d-ae54-4c8d-8d3f-21e7ddcfa00a"/>
</p>

<p>Go back to the Client computer and close the remote desktop session for jane_admin.</p>
<p>Login with the new john_user account to verify a normal user can login from the client computer.</p>
