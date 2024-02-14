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

