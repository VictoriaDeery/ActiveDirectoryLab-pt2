<h1>Active Directory Lab - pt 2</h1>

 ### [YouTube Demonstration-available upon request]
 
<h2>Description</h2>
This lab consists of a walkthrough for a few common scenarios using Active Directory. We will work on dealing with Account Lockouts, Enabling and Disabling Accounts, Observing authentication and security Logs, and Group Policy.
<br />
noteeeee here do we "- Coming Up!: In the next repository, we will reset users' passwords, create network shares, and assign permissions to them based on certain users and groups for permission understanding in AD." otherwise its the next repo but need to change that in first ad lab along w windows 2022 and envi/softwares $$$$$$$

<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Azure</b>
- <b>Active Directory</b>
- <b>remote desktop</b>
- <b>Active Directory Users and Computers</b> 

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)
- <b>Windows 2022</b>

<h2>Outline:</h2>

-  A. Dealing with Account Lockouts
-  B. Enabling and Disabling Accounts
-  C. Observing authentication and security Logs
-  D. Group Policy

<h2>Steps:</h2>

-  A. Dealing with Account Lockouts
  <p>
   group policy, account lockout configuration via group policy.
use dc-1, right-click start, go to run, type gpmc.msc for the group policy management console. In GPMC navigate to group policy objectsby expanding gpm -> forest... ->domains ->mydomain.com and we'll use the "default domain policy" under our mydomain.com. ->new or in this case, right-click default domain policy under our domainan existing GPO ->edit. select "computer config to expand it -> policies -> windows settings -> security settings -> account policies ->lockout policies. from there we can configure: how long the account is locked out before auto-unlock (account lockout duration), number of attempts to trigger lockout (account lockout threshold), and reset account lockout timer. set lockout duration to 30min
</p>
![image](https://github.com/user-attachments/assets/d50e372f-7c4d-4e70-aabd-a71693244eca)

  1. log into dc-1 with any user, 11 times with the wrong password to generate logs and force lock out. Now typing the correct password, we would expect to be locked out for so many failed attempts, but we are notlocked out...yet. So we will use Group Policy to configure the domain password lockout policy. From there we update the  Account Lockout policy in AD using group policy .log into dc-1 with jane_admin and open Active Diretory Users and Computers. in _EMPLOYEES find the user who had failed passwords by name. double click the user name then go to account



-  B. Enabling and Disabling Accounts
-  C. Observing authentication and security Logs
-  D. Group Policy
  </p>
  1. Log into dc-1 as domain admin and open PowerShell Ise as admin by right-clicking it. copy the code from the file at the top of this repository titled "Generate-Names-Create-Users" then back in Powershell create a new file by clicking the first icon below "file", paste it in there and then type ctrl+s to save it to the desktop calling it "create-users" hit the green arrow to run the script to generate users.

  
 - H. Confirm by logging into the Windows 10 computer using a normal domain user, which we will create)
   <p>
<img src="https://github.com/user-attachments/assets/4dccc062-34a1-4659-9f95-25dd70af1436" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 </p>
  1. Every user being created will have the specified "Password1" password unless you change that in the script. If you click into the OU "_EMPLOYEES" you will now see many users. Select a random user For example, I choose topuh.goto. (If you double-click a user and select "member of," you'll see that by default, they are a member of the domain users, which is the group we allowed remote access for in a previous step. Close client-1's connection with Jane Doe. Log in to client-1 with the username mydomain.com\topuh.goto, and if you open the command prompt, you will see there is a local profile on this computer for topuh.goto. And if you select file explorer -> this PC -> Windows (C:) drive -> users, you will see all users that logged in. You may sign out of client-1
   <p>











 <br />
Select the disk:  <br/>
<img src="https://i.imgur.com/tcTyMUE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for the process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
