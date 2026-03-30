<p align="center">
<img width="849" height="436" alt="image" src="https://github.com/user-attachments/assets/9b7bb3b5-b0d5-4419-94a5-4f4f5bd0b8f2" />
</p>

<h1>Designing Active Directory Infrastructure in Azure</h1>
This section of the lab involves building the foundational cloud infrastructure required for an Active Directory environment in Microsoft Azure. The process included creating a resource group, deploying a virtual network, provisioning virtual machines for the domain controller and client, and validating network connectivity to ensure the environment was ready for domain services deployment.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Azure Virtual Network
- Azure Resource Groups
- Remote Desktop Protocol (RDP)
- DNS

<h2>Operating Systems Used </h2>

- Windows Server 2022 (Standard_D2s_v3 - 2 vcpus, 8 GiB memory)
- Windows 11 pro (Version 25H2 - x64 Gen2)

<h2>Open Resource Groups in Azure</h2>

<p>
<img width="1461" height="896" alt="Lab1" src="https://github.com/user-attachments/assets/f6d5d6c0-a4d6-45ff-a25a-3a674006834e" />
</p>
<p>
 Step-by-step

1. Sign in to the **Azure portal**
2. Navigate to Resource groups from the Azure services menu
3. Select **Create** to begin building a new resource group for the lab environment

**Explanation:** 
 A resource group is used to organize related Azure resources in one location. Creating it first helps keep all lab components structured and easier to manage.

<h2>Create the Resource Group</h2>

<img width="1512" height="982" alt="Lab2" src="https://github.com/user-attachments/assets/55239797-f727-4e73-998f-55116d0ad19b" />
</p>
<p>
Step-by-step
  
1. Select the appropriate Azure subscription
2. Enter the resource group name **Active-Directory-Lab**
3. Chose the region Canada Central
4. Click **Review + Create** 
5. Continue to create the resource group

**Explanation:**
 This created a dedicated container for all resources used in the lab, including virtual machines and networking components.

<h2>Create the Virtual Network</h2>

<img width="1512" height="982" alt="Lab4" src="https://github.com/user-attachments/assets/a896cf84-a1c0-49f1-b743-ee076abb921c" />
</p>
<p>
Step-by-step

1. Open Virtual networks in Azure
2. Select **Create**
3. Assign the network to the Active-Directory-Lab resource group
4. Enter the virtual network name **Active-Directory-VNet**
5. Confirm that the region is the same as the resource group
6. Review the default IP address space and subnet settings
7. Click **Create**

**Explanation:**
 The virtual network allows the domain controller and client machine to communicate privately inside Azure. This is required for domain communication and DNS resolution.

<h2>Begin Creating the Domain Controller VM</h2>

<img width="1512" height="982" alt="Lab5" src="https://github.com/user-attachments/assets/9a1f8302-0947-4b6f-9eac-ef67c879d614" />
<p>
Step-by-step

1. **Open** Virtual machines in Azure
2. Click **Create virtual machine**
3. Select the **Active-Directory-Lab resource group**
4. Enter the **VM name dc-1**
5. Select the deployment region (Canada Central)
6. Review the basic configuration settings

**Explanation:**
 This virtual machine is created to serve as the main server for the lab. It would later be promoted to a Domain Controller.

<h2>Configure dc-1 Operating System and Credentials</h2>

<img width="1512" height="982" alt="Lab6" src="https://github.com/user-attachments/assets/54c07d12-6741-4d63-8e40-4887fb3ef0ce" />
</p>
<p>
Step-by-step

1. Select **Windows Server 2022 Datacenter Azure Edition** as the image
2. Confirm the VM architecture setting 
3. Select the **VM size** for the lab
4. Enter the **administrator username**
5. Enter and confirm the **administrator password**
6. Continue through the setup wizard

**Explanation:**
 This step ensures that the server is deployed with a supported Windows Server operating system capable of running Active Directory Domain Services.

<h2>Configure Networking for dc-1</h2>

<img width="1512" height="982" alt="Lab7" src="https://github.com/user-attachments/assets/101e4773-24e6-43f7-944d-b857841d7bfe" />
</p>
<p>
Step-by-step

1. Open the Networking tab during the dc-1 VM creation
2. Select **Active-Directory-VNet** as the virtual network
3. Keep the **default subnet**
4. Assign a public IP address for remote access
5. Set the network security group options
6. Allow **RDP (3389)** inbound access
7. Review the settings before deployment                                   

**Explanation:**
 This configuration integrates DC-1 into the lab network infrastructure and enables secure remote management using Remote Desktop Protocol (RDP).

<h2>Configure DC-1 Private IP Address</h2>

<img width="1512" height="982" alt="Lab12" src="https://github.com/user-attachments/assets/7d19e742-f66f-4321-bd6b-2bea5dc48323" />
</p>
<p>
Step-by-step

1. Navigate to the Network Interface settings for the DC-1 virtual machine
2. Selecte **IP configurations** to modify the network settings
3. Open the primary IP configuration **ipconfig1**
4. Change the Private IP allocation setting from **Dynamic to Static**
5. Verify the assigned private IP address **10.0.0.4**
6. Confirm the public IP address association for remote access
7. Than save the configuration changes

**Explanation**
 This step ensures that the DC-1 domain controller maintains a consistent private IP address, which is critical for reliable DNS services and proper communication within the Active Directory environment.

<h2>Begin Creating the Client VM</h2>

<img width="1512" height="982" alt="Lab8" src="https://github.com/user-attachments/assets/3445cc72-d890-4b3d-ba6b-84c7d24071d9" />
</p>
<p>
Step-by-step

1. Create another virtual machine process
2. Select the **Active-Directory-Lab resource group**
3. Enter the virtual machine name **Client-1**
4. Choose the same region as dc-1 **Canada Central**
5. Review the basic configuration settings

**Explanation:**
 This machine was created to simulate a workstation that would later connect to and join the domain.

<h2>Configure Client-1 Operating System and Credentials</h2>

<img width="1512" height="982" alt="Lab9" src="https://github.com/user-attachments/assets/8fda5b9d-1710-4884-9f1d-6f48963d5086" />
</p>
<p>
Step-by-step

1. Select **Windows 11 Pro** as the virtual machine image.
2. Confirm the VM architecture for compatibility.
3. Select the appropriate **VM size** for the lab environment.
4. Enter the **administrator username** for the client machine.
5. Enter and confirmed the **administrator password.**
6. Continue through the Azure VM creation wizard to proceed with deployment.

**Explanation:**
 This step ensured that the client computer was deployed with a supported Windows operating system that will later be connected to the DC-1 domain controller as part of the Active Directory environment.

<h2>Configure Networking for Client-1</h2>

<img width="1512" height="982" alt="Lab10" src="https://github.com/user-attachments/assets/d4ea39a7-1c08-45fe-bf5a-1b9e13b2503f" />
</p>
<p>
Step-by-step

1. Open the Networking tab during the Client-1 setup
2. Select **Active-Directory-VNet**
3. Keep the **default subnet**
4. Assign a public IP address
5. Configure the network security settings
6. Allow **RDP (3389)** inbound access
7. Continue with the deployment

**Explanation:**
 This Comfirms that Client-1 was on the same virtual network as dc-1 so both machines could communicate internally.

<h2>Verify Both Virtual Machines Are Running</h2>

<img width="1512" height="982" alt="Lab13" src="https://github.com/user-attachments/assets/0506e0a0-f236-40a7-b858-6e5191fedd34" />
</p>
<p>
Step-by-step

1. Return to the Virtual machines page
2. Verify that dc-1 and Client-1 appeared in the list
3. **Confirm** both virtual machines shows a Running status

**Explanation:**
 This confirms that both systems were deployed successfully and were ready for configuration and testing.

<h2>Connect to dc-1 with Remote Desktop</h2>

<img width="1512" height="982" alt="Lab14" src="https://github.com/user-attachments/assets/67686dfb-668a-4d11-b359-9a2881ba7472" />
</p>
<p>
Step-by-step

1. Open the **dc-1 virtual machine details in Azure**
2. Locate the public IP address for dc-1   
3. Open **Remote Desktop** Connection on the local computer
4. Enter the **public IP address**
5. Enter the **administrator credentials**
6. Now start the remote session

**Explanation:**
 Remote Desktop provides administrative access to the server so configuration tasks can be completed directly inside the VM.

<h2>Verify Server Manager on dc-1</h2>

<img width="1512" height="982" alt="Lab16" src="https://github.com/user-attachments/assets/1c6b44d7-a7f5-42e2-af14-626bd5b40532" />
</p>
<p>
Step-by-step
 
1. Connect to dc-1 using Remote Desktop Protocol.
2. Allow the Windows Server desktop to fully load.
3. **Confirm** that Server Manager opened successfully, indicating the server was ready for configuration.

**Explanation:**
 Server Manager is the main administrative tool used to install server roles and manage Windows Server services.

<h2>Adjust Windows Firewall Settings for Lab Testing</h2>

<img width="1512" height="941" alt="Lab19" src="https://github.com/user-attachments/assets/87a8f4ac-8441-4e6f-8ee4-7428634825cd" />
</p>
<p>
Step-by-step

1. Open Windows Defender Firewall with Advanced Security on dc-1.
2. Review the firewall profile settings.
3. Adjust the firewall configuration for the lab environment.
4. **Confirm** the changes were applied.

**Explanation:**
 In a lab environment, firewall settings are sometimes adjusted to make connectivity testing easier between systems.This helps avoid blocked communication during setup and troubleshooting.

<h2>Begin Connectivity Testing from Client-1</h2>

<img width="1512" height="982" alt="Lab23" src="https://github.com/user-attachments/assets/b606bba2-f30e-4fc5-a8ec-01499e9e183d" />
</p>
<p>
Step-by-step

1. Log into **Client-1**
2. Open Windows PowerShell
3. Enter the following command: **ping 10.0.0.4**
4. Run the command to test connectivity to the domain controller
 
**Explanation:**
 This test verifies network connectivity between Client-1 and the domain controller (DC-1). Successful ping responses confirm that the client machine can reach the server across the private network.

<h2>Verify Network Connectivity and DNS Settings</h2>

<img width="1512" height="982" alt="Lab24" src="https://github.com/user-attachments/assets/078966a3-eeb8-4d37-bd2e-d3f1c57f41ae" />
</p>
<p>
Step-by-step

1. Confirm that the ping to **10.0.0.4** was successful
2. Enter the following command: **ipconfig /all**
3. Review the network adapter details
4. Verify the client IP configuration
5. Confirm the DNS server setting points to **10.0.0.4**

**Explanation:**
 This final verification confirmed that Client-1 could communicate with dc-1 and that the DNS settings were correctly configured to point to the domain controller. That completes the infrastructure setup required before deploying Active Directory.

<h2>Server Manager Dashboard</h2>

<img width="1512" height="982" alt="LabA1" src="https://github.com/user-attachments/assets/007229ca-16b8-4a2e-a433-0f1cfdddc5c5" />
<p>
<p>
Step-by-step
 
1. Open the **Windows Server virtual machine dc-1.**
2. Log into the server using administrative credentials.
3. Wait for the desktop environment to finish loading.
4. Open **Server Manager.**
5. Review the dashboard to confirm the server is available for configuration.
6. Prepare to begin installing the Active Directory Domain Services role.


**Explanation:** 
 This shows the starting point of the server configuration process. Server Manager is the primary tool used to install roles and features on Windows Server, including Active Directory Domain Services.

<h2>Select Active Directory Domain Services</h2>

<img width="1512" height="982" alt="LabA4" src="https://github.com/user-attachments/assets/ce674a69-e3b4-46b8-bf36-3fd53eff97f5" />
</p>
<p>
Step-by-step

1. Select **Add Roles and Features.**
2. Continue through the wizard until reaching the Server Roles page.
3. Locate Active Directory Domain Services in the list of available roles.
4. **Check the box for Active Directory Domain Services.**
5. Review the description shown on the right side of the wizard.
6. Prepare to continue with the required supporting features.

**Explanation:**
 Installing the Active Directory Domain Services role does not automatically create a domain. At this stage, the role is installed, but the server must still be promoted to a Domain Controller before it can manage users,computers, and authentication. 

<h2>Confirm Installation Selections</h2>

<img width="1512" height="982" alt="LabA10" src="https://github.com/user-attachments/assets/5c2b0f8a-0beb-47e2-b0f8-fd373731036d" />
</p>
<p>
Step-by-step

1. Accept the additional required features when prompted.
2. Continue through the wizard until reaching Confirm installation selections.
3. Review the selected roles and features, including:
-  **Active Directory Domain Services**
-  **Group Policy Management**
-  **Remote Server Administration Tools**
4. Check **Restart the destination server automatically if required.**
5. Click **Install.**

**Explanation:**
 At this stage, the server confirms the installation of the required components for Active Directory Domain Services. This installation is an important step toward configuring the Windows Server to operate as a Domain Controller.

<h2>AD DS Installation Complete</h2>

<img width="1512" height="982" alt="LabA13" src="https://github.com/user-attachments/assets/5bb8cc35-3cc1-44ed-adeb-55284ff6802d" />
</p>
<p>
Step-by-step

1. Wait for the role installation process to finish.
2. Review the completion message in the wizard.
3. Confirm that the message indicated:
   **Configuration required, Installation succeeded on dc-1**
4. Read the notice explaining that further steps are needed to make the machine a domain controller.
5. Locate the link:
   **Promote this server to a domain controller**
6. Prepare to continue post-deployment configuration.

**Explanation:**
   After installing the Active Directory Domain Services role, a domain is not created immediately. The role is available on the server, but the system must still be promoted to a Domain Controller in order to begin managing users, computers, and authentication within the network.

<h2>Promote This Server to a Domain Controller</h2>

<img width="1512" height="982" alt="LabA14" src="https://github.com/user-attachments/assets/f183fcc9-90fe-4761-8a2e-792561fff437" />
</p>
<p>
Step-by-step

1. Return to the Server Manager dashboard after the AD DS role finished installing.
2. Observe the notification flag in the upper-right corner.
3. Click the **notification flag.**
4. Review the post-deployment message indicating that configuration is required for Active Directory Domain Services on dc-1.
5. Locate the option:
  **Promote this server to a domain controller**
6. Select the **promotion link** to begin the Active Directory Domain Services Configuration.

**Explanation:**
 This step begins the second stage of the deployment. The server now has the AD DS role installed, and this post-deployment task starts the process of creating the domain and promoting the server into a Domain Controller.

<h2>Configure a New Forest</h2>

<img width="1512" height="982" alt="LabA15" src="https://github.com/user-attachments/assets/eddba04a-5b9a-498f-ba3b-5023ef30a5b3" />
</p>
<p>
Step-by-step

1. Open the Active Directory Domain Services Configuration Wizard from Server Manager.
2. Review the available deployment options.
3. Select **Add a new forest.**
4. **Click** into the Root domain name field.
5. Enter the domain name: **mydomain.com**
7. Verify that the new forest option was selected.
8. Click **Next** to continue.

**Explanation:**
 This step creates a brand-new Active Directory forest and defines the root domain name. The forest is the top-level structure of Active Directory, and the root domain becomes the main administrative boundary for the environment.

<h2>Configure Domain Controller Options</h2>

<img width="1512" height="982" alt="LabA16" src="https://github.com/user-attachments/assets/4e983d81-ec42-452e-9f1e-3f1944a90681" />
</p>
<p>
Step-by-step

1. Continue to the Domain Controller Options page.
2. Review the default Forest functional level.
3. Review the default Domain functional level.
4. Verify that the DNS server option was selected.
5. Verify that the Global Catalog (GC) option was enabled.
6. Leave **Read only domain controller (RODC)** unselected.
7. Enter a **Directory Services Restore Mode (DSRM)** password.
8. Confirm the DSRM password in the second field.
9. Click **Next** to continue.

**Explanation:**
 This stage sets essential configuration settings for the Domain Controller. It verifies the server’s role, installs Domain Name System support for name resolution, and creates the DSRM password, which is required to access recovery mode for troubleshooting or restoring Active Directory.

<h2>Prerequisites Check</h2>

<img width="1512" height="982" alt="LabA19" src="https://github.com/user-attachments/assets/d2ae020f-3381-4542-af63-d968ec968d0a" />
</p>
<p>
Step-by-step

1. Continue through the configuration wizard after reviewing the deployment options.
2. Reach the Prerequisites Check page.
3. Wait while Windows validates the configuration.
4. Review the results shown in the wizard.
5. Confirm the message stated:
**All prerequisite checks passed successfully**
6. Review the warning messages listed in the results panel.
7. Verify that no blocking errors prevented the promotion process.
8. Click **Install for Installation**

**Explanation:**
 This step performs a readiness check before the server is promoted to a Domain Controller. The wizard reviews system requirements, verifies that all necessary components are installed, and displays any warnings or issues that must be addressed before continuing.

<h2>Domain Controller Promotion Complete</h2>

<img width="1512" height="982" alt="LabA21" src="https://github.com/user-attachments/assets/32ac0b77-0ff4-4d0a-96a5-3e059b152a46" />
</p>
<p>
Step-by-step

1. Wait while Active Directory is configured.
2. Review the Results page after the promotion process completes
3. Verify the message stating:
**This server was successfully configured as a domain controller**
4. Observe the notification indicating that the computer is about to be signed out.
5. Read the restart message explaining that:<br>
**The server is restarting because Active Directory Domain Services is being installed or removed**
7. Allow the restart process to continue.

**Explanation:**
 This step confirms that the server was successfully promoted to a Domain Controller. A restart is required to finalize the Active Directory configuration and to bring the domain services online.

<h2>Server Manager After Restart</h2>

<img width="1512" height="982" alt="LabA24" src="https://github.com/user-attachments/assets/207cef9d-d2eb-4df3-85eb-bcf46e38c946" />
</p>
<p>
Step-by-step

1. Wait for dc-1 to restart after Domain Controller promotion.
2. Log back into the server.
3. Open Server Manager.
4. Review the dashboard after the restart completes
5. Confirm that the left navigation panel now displays:<br>
***AD DS**<br>
***DNS**
6. Verifiy that the new roles appeared as active components of the server.

**Explanation:**
 This step verifies that the server restarted successfully after the promotion process. It confirms that Active Directory Domain Services and DNS are now running as installed roles, indicating the domain controller setup is complete.
 
<h2>Verify Domain Presence in Active Directory Users and Computers</h2>

<img width="1512" height="982" alt="LabA26" src="https://github.com/user-attachments/assets/86c56d9d-c2e9-46dd-9aa7-139cf9f9a593" />
</p>
<p>
Step-by-step

1. Click **The Start/Menu**
2. Click **Windows Administrative Tools**
3. On the drop down **Select Active Directory Users and Computers**
4. Confirm that **mydomain.com** appears under Active Directory Users and Computers.
5. Verify that the domain is listed and accessible in the console.

**Explanation:**
 This step confirms that the Active Directory domain was successfully created and now is visible within the Active Directory Users and Computers management console. Seeing the domain listed indicates that the Domain Controller is properly managing the new directory environment and that administrators can begin managing users, computers, and organizational units within the domain.

<h2>Create Organizational Unit</h2>

<img width="1512" height="982" alt="LabA27" src="https://github.com/user-attachments/assets/e5533823-69e2-426f-81b2-14f2859f84e6" />
</p>
<p>
Step-by-step

1. Open Active Directory Users and Computers.
2. Select the **mydomain.com**.
3. Right-click the domain name.
4. Choose New.
5. Select **Organizational Unit.**
6. Click into the Name field.
7. Enter the name:
  **_EMPLOYEES**
8. Leave **Protect container from accidental deletion** Checked.
9. Click OK to create the Organizational Unit.

**Explanation:**
 This step creates an Organizational Unit to help organize user accounts in the domain. OUs are useful for administrative structure and applying policies to groups of users or computers.

<h2>Create New User Account</h2>

<img width="1512" height="982" alt="LabA28" src="https://github.com/user-attachments/assets/2e3f60de-e279-4f07-b20f-de2de742fcbd" />
</p>
<p>
Step-by-step

1. Open Active Directory Users and Computers.
2. Select the target Organizational Unit for the user account.
3. Right-click the OU.
4. Choose **New.**
5. Select **User.**
6. Enter the user’s first name:
         **Jane**
7. Enter the user’s last name:
         **Doe**
8. Review the automatically generated full name.
9. Enter the user logon name.
10. Review the **pre-Windows 2000** logon name.
11. Click Next to continue user creation.

**Explanation:**
 This step creates a new Active Directory user account. Creating users in Active Directory allows administrators to manage authentication, access permissions, and organizational membership centrally.

<h2>Verify User Account Creation</h2>

<img width="1512" height="982" alt="LabA29" src="https://github.com/user-attachments/assets/43164a28-592c-4807-ae7c-7dc234b77b58" />
</p>
<p>
Step-by-step

1. Complete the New User wizard.
2. Return to **Active Directory Users and Computers**.
3. Select the OU where the user was created.
4. Review the right panel.
5. Confirm that the new account appeared in the directory listing.
6. Verify that the account name displays as:
            **Jane Doe**
7. Confirm the object type shows **User**.

**Explanation:**
 This step verifies that the user account was successfully created in Active Directory. Seeing the account in the directory confirms that the Object now exists and can be managed like any other domain user.

<h2>Add User to Domain Admins</h2>

<img width="1512" height="982" alt="LabA30" src="https://github.com/user-attachments/assets/ce03b23c-4869-4133-85da-91fb76784e5a" />
</p>
<p>
Step-by-step

1. Right click the user created.
2. Click **Properties** in the drop down.
3. Navigate to the **Member Of** tab.
4. Select **Add.**
6. Click into the object name field.
7. Enter: **Domain Admins**
8. Press **Check Names**
9. Than click **OK.**

**Explanation:**
 This step assigns the user administrative privileges by adding the account to the Domain Admins group. Group membership is a common way to manage permissions and administrative roles in Active Directory.

<h2>Join Client-1 to the Domain</h2>

<img width="1512" height="982" alt="LabA31" src="https://github.com/user-attachments/assets/e697b803-9c35-4142-991c-d52c683ca6ec" />
</p>
<p>
Step-by-step

1. Log into the Client-1 virtual machine.
2. Open start/meanu and select **System**.
3. Navigate to **Rename this pc (advanced)**
4. Under Computer Name tab Click on **Change**
5. View Computer Name/Domain Changes window that will open.
6. Select the Domain option under Member of.
7. Click into the domain field.
8. Enter: **mydomain.com**
9. Than click OK

**Explanation:**
 This step begins the process of joining the client machine to the Active Directory domain. Joining a workstation to the domain allows centralized login, management, and policy enforcement from the Domain Controller.

<h2>Restart Client-1 After Domain Join</h2>

<img width="1512" height="982" alt="LabA34" src="https://github.com/user-attachments/assets/7af4649a-757e-481f-b0dd-8cdc38e7112b" />
</p>
<p>
Step-by-step

1. Enter the **domain name** on Client-1.
2. Authenticate with domain credentials when prompted.
3. Accept the restart prompt.
4. Allow Client-1 to begin restarting.
5. Wait till the restart process is completed.

**Explanation:**
 A restart is required after joining a computer to a domain. This allows Windows to apply the new domain membership and finalize communication with the Domain Controller.

<h2>Verify Client-1 in Active Directory</h2>

<img width="1512" height="982" alt="LabA35" src="https://github.com/user-attachments/assets/16cae8d8-18ca-431a-9ffb-04c8385ae50c" />
</p>
<p>
Step-by-step

1. Return to dc-1 after the client restart.
2. Open **Active Directory Users and Computers**.
3. Expand the **mydomain.com** domain.
4. Select the **Computers container**.
5. Review the objects listed in the right panel.
6. Confirm that Client-1 appeared as a Computer object.
7. Open the **Computer object properties** to verify the name and DNS information.

**Explanation:**
 This step confirms that the client workstation successfully joined the domain. Once the computer object appears in Active Directory, the Domain Controller can manage it as part of the domain environment.

<h2>Conclusion</h2>
 At the conclusion of this phase, the Active Directory environment is fully operational. The server is promoted to a Domain Controller, the domain structure is verified, and administrative organization is improved through the creation of an Organizational Unit. The Windows client machine is successfully connected to the domain, demonstrating proper communication between systems 
