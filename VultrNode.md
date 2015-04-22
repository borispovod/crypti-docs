# Setting up Your Crypti Node on a  Cloud Server/ Vultr using  Windows

----------

##1. Register for an Vultr account 
**First you will need to** [register](https://www.vultr.com/)  

  - Setup Billing information

##2. Set up a SSH key

**First download both of these files**

 [PuTTYgen](http://the.earth.li/~sgtatham/putty/latest/x86/puttygen.exe)   
 [PuTTY ](http://the.earth.li/~sgtatham/putty/latest/x86/putty.exe)  

Next you can either **Click this YouTube** below or **Continue** to the next step in writing
[![IMAGE](http://img.youtube.com/vi/ZL5i76iOvXQ/0.jpg)](http://www.youtube.com/watch?v=ZL5i76iOvXQ)

*Note This is for (Digital Ocean) However the steps are very similar at Vultr*

**First we must create a SSH key**

Open **PuTTYgen**

**Then click**

    Generate

**At this point you must mover your mouse around in the blank area**

    Then Copy the whole string of characters

**Save your key**

    Call it something you will remember we need it later

**Now go back to your Vultr account in your web browser, navigate to the [Deploy](https://my.vultr.com/deploy/) Tab**

**Then scroll to the bottom of the screen, and then click [“Manage”](https://my.vultr.com/sshkeys/)SSH Keys**

**Then click**

[Add SSH Keys](https://my.vultr.com/sshkeys/manage.php?SSHKEYID=new)

**Name your key**

**Paste in the long string of characters in the big open Box**
**Then click**

    Add SSH key

##3. Set up your cloud server    

**Navigate back to the [Deploy](https://my.vultr.com/deploy/) Tab**

**Select server Type (PERFORMANCE SERIES)**

**Select server location** 

    New York / New Jersey 
*We seem to be getting the best results with the New York servers, however your results may vary choose whatever location you feel is best*

**Select the OS:** 

    Ubuntu Server 14.04 x64

**Select server size** 

    1CPU/768MB ($5/month) 
*This should be good enough to run 1 Delegate, If you plan on running 2 off 1 node Best to pick a bigger server* 

 <a href="url"><img src="http://i.imgur.com/W976hQs.png" align="center" height="500" width="400" ></a>

 **Enable Private Network**   
*This will allow you to synchronize faster with your other nodes, however it's optional and not required to run a Crypti node*

 **Select the SSH Key you just made**

**Label your server**
     
**Click the Blue button**

	Place Order



##4. Access your cloud server from your desktop

Now open **PuTTY**

**In the PuTTY window on the left hand side Click**
   

     SSH
**Then Click** 

    Auth
**Now Click button**

    Browse
**Next Navigate to your ( *.ppk ) Key file saved from PuTTYgen**

     Open it
**On the left hand side at the top Click**

    Session
**Then in the Saved Session box in the middle of the window**

    Label it the same as your Server name
**Then Click**

    Save
**Now go back to your Vultr account in your web browser, under the [My Server](https://my.vultr.com/index.php) Tab**

 - **Your server should be ready, if not just wait**
 - **Then identify your IP address under your server name**

**Copy** 

     IP address


**In the PuTTY window in the Host name (IP address) box**

    Past your IP address

In that same box in front of your **IP address** Type 

    root@
**It should look like this with a space**

    root@ 54.111.111.11
Note: having **"root@"** typed before your IP automatically logs you in as root

**Then Click**

    Save

**Finally at the bottom Click** 

    Open

##4. Follow the Linux install Guide

[Install guide](https://github.com/crypti/crypti-docs/blob/master/install.md)
