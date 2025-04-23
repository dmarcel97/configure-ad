<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Deploy and Configure the Domain Controller 
- Establish Organizational Units and Administrative Accounts
- Join Client Machines to the Domain
- Configure Remote Desktop Access for Domain Users
- Automate User Account Creation and Management

<h2>Deployment and Configuration Steps</h2>



Step 1: Install Active Directory

Log into DC-1(this is what we name the virtual machine that is dealing with the server information) and install Active Directory Domain Services.

Promote DC-1 as a Domain Controller and set up a new forest (e.g., mydomain.com).

Restart the server, then log back in as mydomain.com\yourcomputerusername.

</p>

Step 2: Create a Domain Admin User
Open Active Directory Users and Computers from the start menu.

Create an Organizational Unit (OU) called _EMPLOYEES and another named _ADMINS.

Add a new user: that you would like to have admin access and create the password as well.

Add the admin account to the Domain Admins Security Group.

Log out, then log back in as mydomain.com\yourcomputerusername.

Use the account you just created as your admin account going forward.

</p>

Step 3: Join Client-1 to the Domain
In Azure Portal, set Client-1’s (the machine you are using to access the server. In this example we are using another vitual machine) DNS to the DC’s private IP (already done).

Restart Client-1.

Log in to Client-1 as the local admin and join it to the domain (mydomain.com).

After restart, verify Client-1 appears in ADUC.

Create a new OU (_CLIENTS) and move Client-1 into it.

</p>

Step 4: Manage Virtual Machines

**Additional Configuration Steps**

</p>

Step 5: Enable Remote Desktop for Domain Users

Power on DC-1 and Client-1 in Azure Portal (if off).

Log into Client-1 as mydomain.com\yourcomputerusername.

Open System Properties → Remote Desktop and allow domain users remote access.

Non-administrative users can now log into Client-1 remotely.

For larger deployments, use Group Policy to enable Remote Desktop across multiple systems.

</p>

Step 6: Create Additional Users and Test Login

Log into DC-1 with the admin account you created.

Open PowerShell ISE as administrator.

Create a new file and paste the provided user creation script in Course Careers. (this is what was used in my training to simulate a good amount of employees on the domain I created)

Run the script and observe new users being added in ADUC (_EMPLOYEES).

Attempt to log into Client-1 using one of the new accounts (use the password from the script).




