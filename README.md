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

<h2>Prerequisites</h2>

- Active Directory Lab part 1 https://github.com/VictoriaDeery/ActiveDirectoryLab

<h2>Outline:</h2>

-  A. Group Policy
-  B. Dealing with Account Lockouts
-  C. Enabling and Disabling Accounts
-  D. Observing authentication and security Logs

<h2>Steps:</h2>

-  A. Group Policy: Account lockout configuration via group policy
  <p>
<img src="https://github.com/user-attachments/assets/53a1b861-08fb-4a5e-9d84-1c7019190b88" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p>
1. Use dc-1, right-click start, go to run, type gpmc.msc for the group policy management console. In GPMC navigate to group policy objects by expanding gpm -> forest... ->domains ->mydomain.com and we'll use the "default domain policy" under our mydomain.com. ->new or in this case, right-click default domain policy under our domainan existing GPO ->edit. select "computer config to expand it -> policies -> windows settings -> security settings -> account policies ->lockout policies. from there we can configure: how long the account is locked out before auto-unlock (account lockout duration), number of attempts to trigger lockout (account lockout threshold), and reset account lockout timer. Right click the policy -> Properties -> check "define this property setting" to set account lockout duration to 15 min, set account lockout threshold to 5 (may happen automatically), set "allow admin lockout" to enabled, and set "reset account lockout counter after" to 10 minutes. On the GPO window, under the "settings" tab you can see the reflected changes. The policy will update after 90 minutes, or immediately if you force the policy to refresh by searching for "command prompt" in the windows search and typing "gpupdate /force" in dc-1. It will update the policy and inform you that it has been completed successfully. If you want a more detailed report, open command as an admin, you will see GP wa applied, when, and other information. 
</p>
<img src="https://github.com/user-attachments/assets/d50e372f-7c4d-4e70-aabd-a71693244eca" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://github.com/user-attachments/assets/efadc96d-e38f-4967-92d1-b0c5c164ddec" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p>
 
</p>
-  B. Dealing with Account Lockouts and password resets
 <p>
 
</p>
  1. log out. then log into one of the VMs with any user, 11 times with the wrong password to generate logs and force lock out. Now typing the correct password, we would expect to be locked out for so many failed attempts because of the configuration we set Account Lockout policy AD using group policy in the previous step.
   <p>
<img src="https://github.com/user-attachments/assets/a894fb50-0f6f-431f-b050-12ca12f60299" height="80%" width="80%" alt="Disk Sanitization Steps"/>


  </p>
  2. From there we unlock the account as an admin. Log into dc-1 with jane_admin or labuser and open Active Diretory Users and Computers. Right-click "mydomain.com" -> "find" -> then search by name for the individual account -> "Find now" -> double click the user's username that was populated below -> in the new window select the "account" tab -> "unlock account" -> Apply. You may try logging in as the previous locked user to confirm success.

<p>
 3. To reset passwords: Log into dc-1. Again, go to Active Directory Users and Computers -> right-click mydomain.com "find" -> then search by name for the individual account -> "Find now" -> right-click the user's username that was populated below -> "reset password" ->in the new window you can make the new password and unlock the account too.
 <p>
  
 </p>
 -  C. Enabling and Disabling Accounts
 <p>
 1. Log into dc-1. Again, go to Active Directory Users and Computers -> right-click mydomain.com "find" -> then search by name for the individual account -> "Find now" -> right-click the user's username that was populated below -> "disable account" or "enable account." You can try to login using an enabled account and you will see and error saying the account has been disabled. There is usually a serious reason an account has been disabled and it should not be taken at face value to simply re-enable it.

 </p>
-  D. Observing authentication and security Logs
</p>
<img src="https://github.com/user-attachments/assets/53d3bc87-3a73-4a08-a6cd-02879df19c14" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p>
 
</p>
Using the dc-1 domain controller, in the windows search bar type "eventvwr.msc" to open the event viewer of all the authentication logs. Expand windows logs -> right-click security -> find -> search the user in question -> Find next. Repeating this process on the client machine client-1, you can also view these logs, in addition to "audit failure" and "event ID4625", however you would either need to log in to the client-1 as an admin, or when you get to seeing the eventvwr.msc, riht-click it to run as an admin and then use an admin's credentials for the context. Event ID4625 is a log in failure ID.

  </p>
