###### Written by Tyler Weiss 

#### Deploy Active Directory (GUI)
In this exercise, you’ll deploy Active Directory (AD) on Windows Server 2019, capturing the essence of creating a Windows Domain. Along the way, take at least four screenshots to document key moments.

After deployment, reflect on the process in a brief narrative. Discuss the purpose of each step, highlighting the role of AD in centralizing domain management and enhancing network security. Your explanation should tie the screenshots to the deployment stages, offering insights into the significance of each action and its impact on the network environment.

This reflection will demonstrate not only your technical capability but also your understanding of AD’s pivotal role in network infrastructure.

Exercise 1 uses the writeup:
https://petri.com/how-to-install-active-directory-in-windows-server-2019-server-manager/

Exercise 2 uses the writeup:
https://petri.com/how-to-install-active-directory-in-windows-server-2019-using-powershell/
#### Exercise 1
Two major steps are involved in the  setup process. First is the installation of Active Directory Domain Services (AD DS). The second is the setup of the Domain Controller (DC). A Domain must have at least one DC to manage the Domain. In this exercise the the server we are installing AD DS on will also be the first DC in the domain.

The first step when installing Active Directory Domain Services and setting up the  Domain Controller is to set a static IP address and rename the server. It's important for the Domain Controller to have a reserved IP address so that the Domain Controller can be accessed reliably.

Open the 'Network and Internet' settings window. Click on 'Change adapter options'. Right click on the network the network interface and choose properties on in the menu. Select 'Internet Protocol Version 4' and click the 'Properties' button. Select the 'Use the following IP address' radio button. If the network is using DHCP, choose a static IP address that is outside of DHCP range. Input the subnet mask, default gateway and DNS server of the network. Click the okay and close in the windows to save the settings. All the above information can retrieved using `ipconfig /all` in the command prompt.
![[Pasted image 20240328204733.png]]

The server, which will also be the first DC in the domain, needs to be renamed to something that makes sense. In this example the servers name will be 'DC1'. 

Open the 'Server Manager' and select 'Local Server'. Click the 'Computer Name'. Click the 'Change' button and Input the new computer name then click 'OK'. A popup alert will appear informing you that the computer needs to be restarted for the changes to take place. Click 'OK' and close the 'System Properties' window. Click 'Restart Now' in the popup dialog.
![[Pasted image 20240328212847.png]]

The next step is to install Active Directory Domain Services. Installing AD DS on the local server will allow will allow it to be connected and managed by an active directory. AD DS will allow the management and organization or objects and members. It is the set of software that facilitates the hierarchical relationships between the objects within a domain or forest so that they can be managed. 

Sign in to the server with the Administrator account and open the 'Server Manager'. Click manage and choose 'Add Roles and Features' in the drop down menu. Make sure the 'Role-based or feature-based installation' radio button is selected. 
![[Pasted image 20240328221013.png]]
![[Pasted image 20240328221754.png]]

Adding features and roles will allow the selection of a server and what applications to install on it. We will be installing Active Directory Domain Services. 

Select the server from the server pool in 'Server Selection'. Select the 'Active Directory Domain Services' role along with 'Include management tools (if applicable)'. Click 'Add Features'. 
![[Pasted image 20240328222056.png]]
![[Pasted image 20240328222138.png]]

Read the information under 'AD DS' and proceed to 'Confirmation. Click 'Install'.
![[Pasted image 20240328222551.png]]
![[Pasted image 20240328223505.png]]

The next step is to configure AD DS on the new DC which will the define a Forest and a Domain. The DC actually facilitates the centralized management and network access of a domain. Under alerts choose 'Promote this server to a domain controller'.
![[Pasted image 20240328223937.png]]

Under 'Deployment Configuration' select 'Add a new forest' enter the 'Root domain name'. You should own the top level domain (TLD) but in this example 'controller.com' will be used. Under 'Domain Controller Options' enter a restore password. This password can be used to take the server offline for emergency maintenance, particularly restoring backups of AD objects. Notice that the DC will also serve as the Domain Name System (DNS) server.
![[Pasted image 20240328225608.png]]
![[Pasted image 20240328225823.png]]

Under 'Additional Options' review the NetBIOS domain name and click 'Next'. The NetBIOS domain name is typically the TLD and will be used as the Domain reference when logging in to the network. Review each section and click 'Next'. Once the prerequisite checks are passed click 'Install'. After the installation the server will automatically restart.
![[Pasted image 20240328230510.png]]
![[Pasted image 20240328230922.png]]

After the server reboots sign-in to the domain administrator account. The domain name preceding the account name show that a user is now logging into the domain 'CONTROLLER'.
![[Pasted image 20240328232033.png]]


### Deploying Active Directory (Powershell)
For this assignment, you will set up Active Directory (AD) on Windows Server 2019 using PowerShell commands, giving you hands-on experience with the command line interface. Make sure to take screenshots of each command you use and the success message at the end showing that AD is deployed.

Along with your screenshots, write a short explanation for each PowerShell command you used. Talk about what each command does and why it’s important for setting up your Windows Domain. This part of the assignment will show that you not only know how to do the task but also understand what each step is for.

#### Exercise 2
The previous exercise has a more in-depth description of each step of the deployment process so I will instead be referencing the descriptions in exercise one, assuming that exercise 1 has been reviewed by the reader. I will however restate the following.

Two major steps are involved in the  setup process. First is the installation of Active Directory Domain Services (AD DS). The second is the setup of the Domain Controller (DC). A Domain must have at least one DC to manage the Domain. In this exercise the the server we are installing AD DS on will also be the first DC in the domain.

As stated in the previous exercise we need to set a proper name for the server, which will be our Domain Controller (DC), and a static IP address to make the server reliably available to the AD forest.

Type the following command in powershell to rename the server to 'DC1' or which ever name you choose then restart the server.
```
Rename-Computer -NewName DC1
```
![[Pasted image 20240409120942.png]]

Once logged back in set a static IP address for the server. Type the following command using a proper reserved IP address from your own network. The '--PrefixLength' option is the length of the subnet mask. Note that the network adapter interface is referenced by index. The 'Get-NetAdapter' cmdlet and method 'InterfaceIndex' allows retrieval of this information.
```
New-NetIPAddress –IPAddress 192.168.1.230 -DefaultGateway 192.168.1.1 -PrefixLength 24 -InterfaceIndex (Get-NetAdapter).InterfaceIndex 
```
![[Pasted image 20240409124245.png]]
![[Pasted image 20240409124313.png]]
Using 'hostname' and 'ipconfig' verifies that the proper changes have been made.
![[Pasted image 20240409143120.png]]

Set the preferred DNS server. If this is the going to be the DC then set use the IP address of the DC. The DNS server for my network happens to be '192.168.1.1'. 
```
Set-DNSClientServerAddress –InterfaceIndex (Get-NetAdapter).InterfaceIndex –ServerAddresses 192.168.1.1
```
![[Pasted image 20240409150845.png]]

The next step is to install install Active Directory Domain Services (AD DS). The previous exercise describes the purpose of the AD DS installation and what this collection of software does. The name of the 'WindowsFeature'  that will be installed is 'AD-Domain-Services' and the option '-IncludeManagementTools' makes sure management tools are added as well.
```
Install-WindowsFeature -name AD-Domain-Services -IncludeManagementTools
```
![[Pasted image 20240409143407.png]]
![[Pasted image 20240409143744.png]]

The last step is to configure the DC in a new AD Forest. In the prior exercise we accomplished this by clicking on the alert flag in the Server Manager Interface and selecting 'Promote this server to a domain controller'. As previously stated the '-DomainName' would be the Top Level Domain (TLD) with the root domain and the '-DomainNetBIOSName' usually your TLD. The NetBIOS Name will be name used to refence the domain witch you will see on the login screen once the AD is properly deployed. You will be asked to input a 'SafeModeAdministratorPassword'. For information on what this password is used for refer to exercise 1 but just keep in mind that this password is extremely important. Once the password is input after running the following command type 'Y' to continue configuration of the AD forest.
```
Install-ADDSForest -DomainName controller.com -DomainNetBIOSName CONTROLLER -InstallDNS
```
![[Pasted image 20240409144756.png]]
![[Pasted image 20240409144855.png]]

After the AD Forest and DC are configured the server will automatically restart.
![[Pasted image 20240409145235.png]]

Notice the difference in time saved using powershell vs the GUI. For a better insight and description the the AD deployment process the GUI method may be more beneficial. On the other hand, using powershell is obviously much faster and simpler but you have to know what you want to do exactly. Choose which method most supports your needs.