<p align="center">
<img src="https://i.imgur.com/tuJ3zhI.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket onto Windows 10.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machine)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10 Pro
</b> 

<h2>List of Prerequisites</h2>

- Azure Virtual Machine
- Internet Information Services in Windows
- osTicket Installation files
- Heidi SQL
- Database for osTicket
- Clean up
- Change File Permissions

<h2>Installation Steps</h2>

>**Note**: Create a Windows 10 Virtual Machine (vm) with 2 or 4 virtual CPUS to ensure it will run with mininal hiccups. More virtual CPUs means better multi-tasking and responsiveness, just like with an actual computer.

Let's setup a `virtual machine` (vm) in Microsoft Azure. Click `Virtual Machine` -> `Create` -> `Azure virtual machine`.

<p align="center">
 <img src="https://i.imgur.com/arz13BB.png" height="50%" width="50%" alt="azure vm"/>
</p>
<br />

As we create our vm we will have the option to create a Resource Group. Here we click `create new` to make a Resource Group called "RG-LAB-osTicket" and configure it below.

<p align="center">
<img src="https://i.imgur.com/5K1cGeU.png" height="60%" width="60%" alt="azure vm"/>
</p>
<br />
<p align="center">
<img src="https://i.imgur.com/bNANgjG.png" height="60%" width="60%" alt="azure vm"/>
</p>
<br />

We'll connect to our vm with remote desktop using our vm's `public IPv4 address`.

<p align="center">
<img src="https://i.imgur.com/YrwMdbI.png" height="50%" width="50%" alt="ipv4-public-vm"/><br/>
</p>
<br />

On Windows 10 search for 'remote desktop connection' and this window will pop up. Copy and paste the public IPv4 address into the text space and hit `Connect`.
<p align="center">
<img src="https://i.imgur.com/UV8Clsh.png" height="50%" width="50%" alt="ipv4-public-vm"/><br/>
</p>
<br />

Once connected to our vm we need to enable 'Internet Information Services' (IIS) and 'Common Gateway Interface' (CGI) support. Search `control panel` -> select `uninstall a program` -> click `Turn windows features on or off` and a pop-up will appear where we will turn on IIS and CGI.

<p align="center">
<img src="https://i.imgur.com/YqWmBG2.png" height="50%" width="50%" alt="ISS"/>
</p>
<br />

Next we need to install a few things found in the [**link here**](https://drive.google.com/drive/u/0/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6). After downloading the files we begin by installing 'PHP Manager for IIS' and 'IIS URL Rewrite Module 2' onto our vm.

<p align="center">
<img src="https://i.imgur.com/uOMpIXg.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/BoWSaTV.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>   
</p>

Next we extract 'php-7.3.8-nts-Win32-VC15-x86.zip' and move the extracted folder into the 'root directory'. Rename the folder: "PHP".
>**Note**: To access the 'root directory' open file explorer and click `This PC` -> Click `Windows (C:)` or type `C:\` into the file explorer address bar and hit the `enter` key.

<p align="center">
<img src="https://i.imgur.com/fVG5v4g.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<p>
<br/>

Now we prepare to install the remaining softwares by runnning 'Microsoft Visual C++ Redistributable Package'. This will help prevent software installation errors and possibly resolve some that may have already occured.

<p align="center">
<img src="https://i.imgur.com/E7ay5n5.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<br />

Next we perform a `typical install` of "MySQL" and go through the configuration wizard. We are prompted to create a password. Make sure to save your password because you will need it again later.

<p align="center">
<img src="https://i.imgur.com/tsDhz3l.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/tuezvVp.jpeg" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br/>

Now we will enable the 'PHP manager'. Search `internet information services` -> select `PHP Manager` -> click `Register new PHP version`.

<p align="center">
<img src="https://i.imgur.com/xSrTPWg.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<p>
<br/>

We are prompted to select a 'PHP executable file' which happens to be in the "PHP" folder we created earlier. Select `php-cgi.exe` and click `OK`.

<p align="center">
<img src="https://i.imgur.com/pk8T6tp.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<p>
<br/>

Extract 'osTicket-v1.15.8.zip' and open the extracted folder. Copy 'upload' folder into `C:\inetpub\wwwroot` and rename it to 'osTicket'. 

<p align="center">
<img src="https://i.imgur.com/5OHh4vO.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<p>
<br/>

After that go back to the IIS manager and we should see 'osTicket' in the connections panel: `*virtual machine's name* -> Sites -> Default Web Site -> osTicket`. Click `Enable or disable an extension`. We need to enable some extensions by right-clicking -> select `enable` on the extensions pointed below.

<p align="center">
<img src="https://i.imgur.com/evsT1n2.png" height="50%" width="50%" alt="Disk Sanitization Steps"/><br/>
<img src="https://i.imgur.com/lWgdHK3.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<p>
<br/>

In `C:\inetpub\wwwroot\osTicket\include` rename `ost-sampleconfig.php` -> `ost-config.php`. Right-click -> `properties` -> click `advanced`. 

<p>
<img src="https://i.imgur.com/ACQvBF1.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<br/>

On the new window click `disable inheritance` -> choose `remove all inherited permissions from this object`, which should clear all permission entries from the window. Click `add`.

<p align="center">
<img src="https://i.imgur.com/X6750BM.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/7yrqlk0.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<p>
<br/>

Click `Select a principal` -> type "Everyone" in the textbox -> click `okay`. Check `Full Control` -> click `okay`. Click `okay` on the 'advanced security settings' windows, then click `okay` on the 'properties' windows.

<p align="center">
<img src="https://i.imgur.com/y8hApv1.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
<br/>

Now we should check on our progress. In the IIS manager click the `osTicket` folder. In the 'Manage Folder' pane click `Browse *:80 (http)` and a webpage will appear. It's the osTicket prerequisite page and it will indicate if we meet the requirements for us to install 'osTicket'. Aside from the two bottom features we should be good to proceed by hitting `continue`.

<p align="center">
<img src="https://i.imgur.com/BypWSMB.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
<br/>

We should be brought to this page. We can fill all sections except the 'Database Settings' because we still need to install something else: 'HeidiSQL'.

<p align="center">
<img src="https://i.imgur.com/P4mQsWS.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
<br/>

>**Note**: Download the HeidiSQL installer from the link provided in the 'HeidiSQL_12.3.0.6589_Setup.exe.docx' file in case you haven't already.

We run the installer and lauch HeidiSQL. Once launched we click `New`. On the next window verify username which should be 'root' and password which should be the password you created for 'mySQL'. Click `Open`.

<p align="center">
<img src="https://i.imgur.com/kdLsa00.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
<br/>

Right-click `Unnamed` -> go to `Create new` -> `Database`. We configure it as shown below and click `Ok`.

<p align="center">
<img src="https://i.imgur.com/qkvY3Wr.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
<br/>

Now we can fill in the 'Database Settings' section and install osTicket.

<p align="center">
<img src="https://i.imgur.com/87kEh1m.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
<br/>

The installation was successful! However we need to do some cleaning up to make sure things run smoothly. First we need to revoke write permissions from the `ost-config.php` file. Below is how I did it.

<p align="center">
<img src="https://i.imgur.com/NllkL6f.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
<br/>

After that we need to delete `C:\inetpub\wwwroot\osTicket\setup`.

<p align="center">
<img src="https://i.imgur.com/qCDDRqW.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
<br/>

And now we login into osTicket via browser. You access the login page by clicking `Your staff control panel` or `Your osTicket URL` links.

<p align="center">
<img src="https://i.imgur.com/pyEja1v.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/p5dxVhg.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/99vluVg.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<p>
<br/>

 <p align="center"><i><b>WE DID IT! Congrats for making it through this tutorial! First time can be rough but after that it's so much easier. 😁</i></b></p>
