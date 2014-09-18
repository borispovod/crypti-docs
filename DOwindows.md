# Setting up Your Crypti Node on a  Cloud Server/ DO (Digital Ocean) using  Windows

----------

##1. Register for an Digital Ocean account 
**First you will need to** [register](https://cloud.digitalocean.com/registrations/new)  

 - Confirm your email
 - Setup Billing information

##2. Set up a SSH key

**First download both of these files**

 [PuTTYgen](http://the.earth.li/~sgtatham/putty/latest/x86/puttygen.exe)   
 [PuTTY ](http://the.earth.li/~sgtatham/putty/latest/x86/putty.exe)  

Next you can either **Click this YouTube** below or **Continue** to the next step in writing
[![IMAGE](http://img.youtube.com/vi/ZL5i76iOvXQ/0.jpg)](http://www.youtube.com/watch?v=ZL5i76iOvXQ)


**First we must create a SSH key**

Open **PuTTYgen**

**Then click**

    Generate

**At this point you must mover your mouse around in the blank area**

    Then Copy the whole string of characters

**Save your key**

    Call it something you will remember we need it later

**Now go back to your DO account in your web browser**

Then in the Left column click  [SSH Keys](http://the.earth.li/~sgtatham/putty/latest/x86/putty.exe)

**Then click**

    Add SSH Keys

**Label your key**
**Paste in the long string of characters in the big open Box**
**Then click**

    Create SSH key
##3. Set up your cloud server    

**Click the Green button**

    Create
**Name your server (or droplet)**

**Select server size** 

    1GB/1CPU ($10/month)

**Select the OS:** 

    Ubuntu Server 14.04 x64

 **Add SSH Keys:**   

     Select Key you just made
     
**Click the Green button**

    Create Droplet



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

    Label it the same as your Droplet name
**Then Click**

    Save
**Now go back to your DO account in your web browser**

 - **Your droplet should be ready, if not just wait**
 - **Then identify your IP address under your droplet name to the left of the word Active**

**Copy** 

     IP address


**In the PuTTY window in the Host name (IP address) box **

    Past your IP address

In that same box in front of your **IP address** Type 

    root@
**It should look like this with a space**

    root@ 54-111-111-11
Note: having **"root@"** typed before your IP automatically logs you in as root

**Then Click**

    Save

**Finally at the bottom Click** 

    Open

##4. Follow the Linux install Guide

[Install guide](https://github.com/crypti/crypti-docs/blob/master/install.md)
