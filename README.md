<p align="center">
<img src="https://github.com/darrylbartlett/configure-ad/assets/159499839/0ef3d6a9-abb7-490b-aab1-b19002987fd4"/>
</p>

<h1>Active Directory (On-premise) Setup</h1>
This tutorial outlines the setup of on-premise Active Directory, connecting to a client computer, and managing different containers and user accounts.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure for creating a Virtual Machine
- Active Directory (On-premise)

<h2>Operating System Used</h2>

- Windows Server 2022 for a domain controller
- Windows 10 Pro (22H2) for a client computer

<h2>List of Prerequisites</h2>

- Creation of an Azure Virtual Machine (VM) with Windows 10 Pro as a client computer
- Creation of an Azure Virtual Machine (VM) with Windows Server 2022 as a domain controller
    - This domain controller has been setup with a static IP on its virtual network interface card
- Connecting to the VMs using Remote Desktop Connection
<br />

<h2>Installation Steps</h2>

<h3>Enable IIS in Windows</h3>
<p>Open Control Panel and select Programs and Features.</p>
<p>On the left menu, click on 'Turn Windows features on or off'.</p>
<p>
<img src="https://github.com/darrylbartlett/osticket-install/assets/159499839/7b71ffbb-56be-42d4-8c11-8a44279a625e"/>
</p>
<br />
