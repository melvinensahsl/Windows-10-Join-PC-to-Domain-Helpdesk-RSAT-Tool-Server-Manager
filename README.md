<h1>Overview: Lab 4 Windows 10, Join PC to Domain (Helpdesk), RSAT Tool, Server Manager</h1>

This section of my home lab documentation demonstrates the process of **joining a Windows 10 PC to a domain** using **RSAT (Remote Server Administration Tools)** and managing server roles through **Server Manager**. The project covers the steps for configuring a Windows 10 PC to be part of an Active Directory domain, using the RSAT tools to perform administrative tasks, and leveraging Server Manager to manage server roles and features within the domain. 

<h2>Objectives</h2>

- **Join a Windows 10 PC to a domain** as part of a helpdesk setup.
- Install and configure **RSAT tools** on Windows 10 for remote administration of servers and network resources.
- Use **Server Manager** to manage server roles and features in a domain environment.
- Perform basic administrative tasks such as user management and role configuration from a client machine.


<h2>Documentation</h2>

In this home lab, I will demonstrate how to install Windows 10 for a local account and join it to our domain (SimoTech.com). To achieve this, we will create a separate virtual machine for the Windows 10 installation, specifically for our local Help Desk account. Next, we will download and install the RSAT (Remote Server Administration Tools) tools to enable the Help Desk account to access and manage Active Directory.

The process begins with downloading the Windows 10 Installation Media Tool from the official Microsoft website: [Windows 10 Installation Media Tool](https://www.microsoft.com/en-us/software-download/windows10).


1. <p align="center">
   <img src="https://i.imgur.com/GGLAP2t.png" height="100%" width="100%" alt="Disk Sanitization Steps 1"/>
   <br />
   <br />
</p>

Open the media tool installer and click 'Accept.' Next, select 'Create installation media (USB flash drive, DVD, or ISO file) for another PC.' Save the download to your 'Downloads' folder, and you should be able to access it from the VirtualBox ISO.


2. <p align="center">
   <img src="https://i.imgur.com/aoOiXmV.png" height="100%" width="100%" alt="Disk Sanitization Steps 2"/>
   <br />
   <br />

Next, open your VirtualBox application and create a new virtual machine. Click Machine in the top-left corner, then select New.


3. <p align="center">
   <img src="https://i.imgur.com/ysk4pQ8.png" height="100%" width="100%" alt="Disk Sanitization Steps 2"/>
   <br />
   <br />
</p>

Name the virtual machine "Windows 10 Project." For the ISO image, navigate to the Downloads folder, click the dropdown icon, select "Other," and choose the "Windows" ISO file. Then, select "Skip unattended installation.”

4. <p align="center">
   <img src="https://i.imgur.com/uNTfHC7.png" height="100%" width="100%" alt="Disk Sanitization Steps 3"/>
   <br />
   <br />
</p>

Select Hardware, and by default, the base memory is set to 2048 MB. Increase it to 6081 MB. Finally, click Finish and start the machine by pressing Start. On the Windows Setup screen, click Next, then Install Now.

5. <p align="center">
   <img src="https://i.imgur.com/mCEOP68.png" height="100%" width="100%" alt="Disk Sanitization Steps 4"/>
   <br />
   <br />
</p>



5. <p align="center">
   <img src="https://i.imgur.com/BYL5Rab.png" height="100%" width="100%" alt="Disk Sanitization Steps 5"/>
   <br />
   <br />
</p>

Select “I don’t have a product key”.

6. <p align="center">
   <img src="https://i.imgur.com/Cqj4mG2.png" height="100%" width="100%" alt="Disk Sanitization Steps 6"/>
   <br />
   <br />
</p>

Make sure to select "Windows 10 Pro," check the box to accept the license terms, and click Next.

7. <p align="center">
   <img src="https://i.imgur.com/oeoA5gp.png" height="100%" width="100%" alt="Disk Sanitization Steps 7"/>
   <br />
   <br />
</p>

Select "Custom: Install Windows only," then click Next to begin the installation of Windows 10.

8. <p align="center">
   <img src="https://i.imgur.com/G5lwPQs.png" height="100%" width="100%" alt="Disk Sanitization Steps 8"/>
   <br />
   <br />
</p>



9. <p align="center">
   <img src="https://i.imgur.com/L7oAGjD.png" height="100%" width="100%" alt="Disk Sanitization Steps 9"/>
   <br />
   <br />
</p>

Select “Personal use”.

10. <p align="center">
   <img src="https://i.imgur.com/y7SOYBP.png" height="100%" width="100%" alt="Disk Sanitization Steps 10"/>
   <br />
   <br />
</p>

On the bottom left, select “Offline account”.

11. <p align="center">
   <img src="https://i.imgur.com/FXsmpDV.png" height="100%" width="100%" alt="Disk Sanitization Steps 11"/>
   <br />
   <br />
</p>

Enter "User" as the name, skip the password creation, and click Next.

12. <p align="center">
   <img src="https://i.imgur.com/xTaLHq3.png" height="100%" width="100%" alt="Disk Sanitization Steps 12"/>
   <br />
   <br />
</p>

Now we should have our Windows 10 ready. 

13. <p align="center">
   <img src="https://i.imgur.com/h9bVREP.png" height="100%" width="100%" alt="Disk Sanitization Steps 13"/>
   <br />
   <br />
</p>

For best practice in a lab environment, we’ll configure static IP addresses for both virtual machines. This ensures consistent network communication and allows us to successfully connect the Windows 10 machine to the domain, enabling seamless interaction between the two virtual machines.
Next, switch to the Windows Server 2022 virtual machine. Open the Control Panel and go to **View network status and tasks** → **Change adapter settings**. Right-click the network connection (Ethernet) and select **Properties** to begin configuring the network settings.

14. <p align="center">
   <img src="https://i.imgur.com/aU13t2f.png" height="100%" width="100%" alt="Disk Sanitization Steps 14"/>
   <br />
   <br />
</p>



15. <p align="center">
   <img src="https://i.imgur.com/9J5hKgd.png" height="100%" width="100%" alt="Disk Sanitization Steps 15"/>
   <br />
   <br />
</p>



16. <p align="center">
   <img src="https://i.imgur.com/KqPzSri.png" height="100%" width="100%" alt="Disk Sanitization Steps 16"/>
   <br />
   <br />
</p>

Double-click on Internet Protocol Version 4 (TCP/IPv4).

17. <p align="center">
   <img src="https://i.imgur.com/QFfQ3wT.png" height="100%" width="100%" alt="Disk Sanitization Steps 17"/>
   <br />
   <br />
</p>

Select **Use the following IP address**, then configure the static IP address as follows:

- IP Address: 12.1.10.2
- Subnet Mask: 255.0.0.0
- Default Gateway: 12.1.10.1
- Preferred DNS: 12.1.10.2
- Alternate DNS: 12.1.10.1

Click **OK** to save the settings.

18. <p align="center">
   <img src="https://i.imgur.com/FiICk3y.png" height="100%" width="100%" alt="Disk Sanitization Steps 18"/>
   <br />
   <br />
</p>

Next, modify the network settings on the virtual machine by selecting Devices at the top, then choose Network and go to Network Settings.

19. <p align="center">
   <img src="https://i.imgur.com/EJp9450.png" height="100%" width="100%" alt="Disk Sanitization Steps 19"/>
   <br />
   <br />
</p>

Now, change Attached to: NAT to Host-only Adapter.

20. <p align="center">
   <img src="https://i.imgur.com/9jQic9N.png" height="100%" width="100%" alt="Disk Sanitization Steps 20"/>
   <br />
   <br />
</p>

Now, switch back to the Windows 10 Project machine and enable the administrator account. Open File Explorer, right-click This PC, and select Manage. This will open Computer Management.


21. <p align="center">
   <img src="https://i.imgur.com/NFXwVQv.png" height="100%" width="100%" alt="Disk Sanitization Steps 21"/>
   <br />
   <br />
</p>

Expand Local Users and Groups, then select Users. Right-click on Administrator and click Properties.

22. <p align="center">
   <img src="https://i.imgur.com/qO7x14o.png" height="100%" width="100%" alt="Disk Sanitization Steps 22"/>
   <br />
   <br />
</p>

The Account is disabled option is checked by default. Uncheck it, then select Apply and click OK.

23. <p align="center">
   <img src="https://i.imgur.com/b0dKPAy.png" height="100%" width="100%" alt="Disk Sanitization Steps 23"/>
   <br />
   <br />
</p>

Next, click on Administrator again and select Set Password → Proceed. Create a password, then click OK. A prompt will appear confirming that your password has been set.

24. <p align="center">
   <img src="https://i.imgur.com/FFSGzu0.png" height="100%" width="100%" alt="Disk Sanitization Steps 24"/>
   <br />
   <br />
</p>



25. <p align="center">
   <img src="https://i.imgur.com/h0QLYEH.png" height="100%" width="100%" alt="Disk Sanitization Steps 25"/>
   <br />
   <br />
</p>

Now that the Administrator account is enabled and the password is set, log into that account by first signing out of your Windows 10 Project machine. Right-click the bottom-left Windows icon, select Shut down or sign out, and then choose Sign out.

26. <p align="center">
   <img src="https://i.imgur.com/5UBuXfD.png" height="100%" width="100%" alt="Disk Sanitization Steps 26"/>
   <br />
   <br />
</p>

Now that the Administrator account is available, we will log into it instead.

27. <p align="center">
   <img src="https://i.imgur.com/yunsvPR.png" height="100%" width="100%" alt="Disk Sanitization Steps 27"/>
   <br />
   <br />
</p>

Since the default 'User' account can be accessed without a password, we will remove it to enhance security and prevent unauthorized access. Open File Explorer, right-click This PC, and choose Manage. Navigate to Local Users and Groups and select Users. To delete the 'User' account, right-click on it and select Delete.


28. <p align="center">
   <img src="https://i.imgur.com/TUzNi7i.png" height="100%" width="100%" alt="Disk Sanitization Steps 28"/>
   <br />
   <br />
</p>

To confirm that the 'User' account has been successfully removed, log out and ensure that the only password-protected account remaining is the 'Administrator' account. We have now successfully set up our local Help Desk account. This procedure removes weak default accounts, enhancing the security of Windows 10.

29. <p align="center">
   <img src="https://i.imgur.com/xtg7be3.png" height="100%" width="100%" alt="Disk Sanitization Steps 29"/>
   <br />
   <br />
</p>

Next, we will download the RSAT tools to enable access to Active Directory on a local level. Type "Optional" in the search bar at the bottom left and click on Add an optional feature, then select Add a feature.


30. <p align="center">
   <img src="https://i.imgur.com/JGuCu02.png" height="100%" width="100%" alt="Disk Sanitization Steps 30"/>
   <br />
   <br />
</p>



31. <p align="center">
   <img src="https://i.imgur.com/BFNHx5S.png" height="100%" width="100%" alt="Disk Sanitization Steps 31"/>
   <br />
   <br />
</p>

Type "RSAT" in the search bar for a quicker search, then install the following 7 features:

- RSAT: Active Directory Certificate Services Tools
- RSAT: Active Directory Domain Services and Lightweight Directory Services Tools
- RSAT: DHCP Server Tools
- RSAT: DNS Server Tools
- RSAT: Group Policy Management Tools
- RSAT: Remote Desktop Services Tools
- RSAT: Server Manager

Click **Install (7)**. Once the installation is complete, restart the virtual machine.

32. <p align="center">
   <img src="https://i.imgur.com/5unWiGZ.png" height="100%" width="100%" alt="Disk Sanitization Steps 32"/>
   <br />
   <br />
</p>



33. <p align="center">
   <img src="https://i.imgur.com/YOuVhfx.png" height="100%" width="100%" alt="Disk Sanitization Steps 33"/>
   <br />
   <br />
</p>

Now that all of our administrative tools are installed, we can verify this by clicking the Windows icon at the bottom left and looking for Windows Administrative Tools.

34. <p align="center">
   <img src="https://i.imgur.com/CfWSSqK.png" height="100%" width="100%" alt="Disk Sanitization Steps 34"/>
   <br />
   <br />
</p>

Now, let's add our PC to the domain SimoTech.com. Before doing that, let's rename our PC to Desktop1. To do this, open File Explorer, right-click on This PC, and select Properties. Then, click on Rename this PC (advanced), followed by Change. In the Computer name field, enter Desktop1, click OK, and then select Restart now.

35. <p align="center">
   <img src="https://i.imgur.com/DYshI70.png" height="100%" width="100%" alt="Disk Sanitization Steps 35"/>
   <br />
   <br />
</p>

After the restart, open Internet Explorer and download Google Chrome from the web. Once Chrome is installed, download the TeamViewer Full Client 64-bit. We will be using TeamViewer in our upcoming homelabs.

36. <p align="center">
   <img src="https://i.imgur.com/vt2o9Tm.png" height="100%" width="100%" alt="Disk Sanitization Steps 36"/>
   <br />
   <br />
</p>



37. <p align="center">
   <img src="https://i.imgur.com/P5mqqXz.png" height="100%" width="100%" alt="Disk Sanitization Steps 37"/>
   <br />
   <br />
</p>

Next, we will set a static IP on our Windows 10 machine, just as we did with the Windows Server 2022 machine, and join it to the domain **SimoTech.com**. As before, open **Control Panel** on your Windows 10 Project machine, select **View network status and tasks**, then **Change adapter settings**. Right-click on the Ethernet connection and select **Properties**, then double-click **Internet Protocol Version 4 (TCP/IPv4)**. Select **Use the following IP address** and enter the following:

- IP Address: 12.1.10.3
- Subnet Mask: 255.0.0.0
- Default Gateway: 12.1.10.1
- Preferred DNS: 12.1.10.2
- Alternate DNS: 12.1.10.1

Next, update the network settings on your virtual machine as we did earlier by selecting **Devices** → **Network** → **Network Settings**, and change **NAT** to **Host-only Adapter**.

38. <p align="center">
   <img src="https://i.imgur.com/ak8VDQm.png" height="100%" width="100%" alt="Disk Sanitization Steps 38"/>
   <br />
   <br />
</p>

Now that our networks and static IPs are set up, let's test the connection by **pinging** our Windows 10 machine from the Windows Server 2022 machine. On the Windows 10 Project machine, open **Command Prompt** and type: ping 12.1.10.2

This is the static IP we set up for the Windows Server 2022 machine.

39. <p align="center">
   <img src="https://i.imgur.com/ZTLjD7u.png" height="100%" width="100%" alt="Disk Sanitization Steps 39"/>
   <br />
   <br />
</p>

Now that we can ping the Windows Server 2022 machine, we can finally join our Windows 10 machine to the SimoTech.com domain. First, open File Explorer, right-click on This PC, and select Properties. Then, click on Rename this PC (advanced), followed by Change. Under Domain, type SimoTech.com.

40. <p align="center">
   <img src="https://i.imgur.com/kvSyE1z.png" height="100%" width="100%" alt="Disk Sanitization Steps 40"/>
   <br />
   <br />
</p>

Next, we will use our Administrator account and password to join the domain. Afterward, a prompt will appear asking us to restart the virtual machine to apply the changes.


41. <p align="center">
   <img src="https://i.imgur.com/4fO3dcH.png" height="100%" width="100%" alt="Disk Sanitization Steps 40"/>
   <br />
   <br />
</p>

To verify that Desktop1 has been successfully added to the SimoTech.com domain, open Active Directory Users and Computers on the Windows Server 2022 machine. Select Computers, and you should see DESKTOP1 listed as part of the domain. Desktop1 will serve as our Helpdesk account.



42. <p align="center">
   <img src="https://i.imgur.com/BzpvJcI.png" height="100%" width="100%" alt="Disk Sanitization Steps 40"/>
   <br />
   <br />
</p>

Next, on the Windows Server 2022 machine, still in Active Directory Users and Computers, select Users, right-click on Helpdesk, and choose Reset Password. Create a new password for the Helpdesk account. Afterward, use this new password to log into the Windows 10 virtual machine.



43. <p align="center">
   <img src="https://i.imgur.com/qudngJH.png" height="100%" width="100%" alt="Disk Sanitization Steps 40"/>
   <br />
   <br />
</p>


Now, we can sign in to the Helpdesk account on our Windows 10 machine. On the login screen, make sure to select Other Users, and then log in using the Helpdesk account credentials.

44. <p align="center">
   <img src="https://i.imgur.com/QDBwoDa.png" height="100%" width="100%" alt="Disk Sanitization Steps 40"/>
   <br />
   <br />
</p>

Congratulations! We have successfully set up Windows 10, joined the PC to the domain, and installed the RSAT tools, google and TeamViewer. You can now search for applications like 'Server Manager' and 'Active Directory Users and Computers,' then pin them to the task bar for quick access by right-clicking and selecting 'Pin to taskbar.

45. <p align="center">
   <img src="https://i.imgur.com/cJ1SIZp.png" height="100%" width="100%" alt="Disk Sanitization Steps 40"/>
   <br />
   <br />
</p>


 👉 [Next Lab 5 : Join Windows 10 to Domain (Local User), Group Policy, RSOP Reports](https://github.com/melvinensahsl/Join-Windows-10-to-Domain-Local-User-Group-Policy-RSOP-Reports/tree/main)
