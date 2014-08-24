# Setting up Your Crypti Node on a  Cloud Server/ AWS (Amazon Web Services) using  Windows

----------

##1. Register for an AWS account 
**First you will need to** [register](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html)  
*Note:* sign up for the EC2 which is  **Free for 1 year**.  It will ask for your credit card *but only changers $1 to check that is real*. Fees apply when you go outside of the free services offered, Please read all the [Terms](https://aws.amazon.com/free/). During the registration, It will also call your phone to make sure its a valid number.




##2. Set up your cloud server

 - [Log in](http://aws.amazon.com/) to your Amazon web services
   account
   

**Then go to your** [Management console](https://console.aws.amazon.com/console/home)

**Under** [Compute & Networking](https://console.aws.amazon.com/ec2/v2/home)  **choose**

    EC2

**Click the blue button**

    Launch Instance

**Select the OS:** 

    Ubuntu Server 14.04 LTS (HVM)

 **Choose an Instance Type:**   

     t2.micro

**Next at the top of the screen click the Tab**
   
     6. Configure Security Group


**At the bottom left click** 

    Add Rule
**In the box in the 3rd column Type**

    6040
**In the box in the 4rd column Select**

    Anywhere
**Now in the lower Right corner click**
 

    Review and Launch
**Now in the lower Right corner click**

     launch
**In the pop-up from the drop down box Select**

    create a new key pair
    
**In the Key pair name Type**

     Anything you would like, you will need to remember it for later when we look for it.

**Next Click**

    Download key pair

**Save it in a location you will remember**
 

    Default is your web browser download folder


##3. Access your cloud server from your desktop

You can either **Click this YouTube** below or **Continue** to the next step in writing
[![IMAGE](http://www.apl.washington.edu/project/lib/images/video/video_thumb_play_icon.png)](http://www.youtube.com/watch?v=5STROm2pk0c)

**First download both of these files**

 [PuTTYgen](http://the.earth.li/~sgtatham/putty/latest/x86/puttygen.exe)   
 [PuTTY ](http://the.earth.li/~sgtatham/putty/latest/x86/putty.exe)  

Next open **PuTTYgen**

**Then Click**

    Load
**Next make sure your in the folder you downloaded your Key in to**  

**Then in the lower right corner in the drop down menu Change**

    (*.ppk) to (All Files)
**Now open the Key ( *.pem ) you downloaded from Amazon when setting up your server**

**Then click**

    OK

**Then click**

    Save private key

**Then click**

    Yes
**Save it as the same Name, only with ( .ppk )**

You can now Close **PuTTYgen**

You will now need to use your browser again, **To access your AWS account** 

**Go to your** 
[EC2 Dashboard](https://console.aws.amazon.com/ec2/v2/home)

**From the left column Select**

    Instances
You will now need to Highlight and coppy your **Public DNS** it will look like this

    ec2-54-111-111-11.es-west-2.compute.amazonaws.com
Now open **PuTTY**

In the Host Name box paste in your **Public DNS**

Next in that same box in front of your **Public DNS** Type 

    ubuntu@
**It should look like this**

    ubuntu@ec2-54-111-111-11.es-west-2.compute.amazonaws.com
**While still in the PuTTY window on the left hand side Click**
   

     SSH
**Then Click** 

    Auth
**Now Click button**

    Browse
Next Navigate to your ( *.ppk ) Key file **Open it**

**Finally at the bottom Click** 

    Open

##4. Follow the Linux install Guide

[Install guide](https://github.com/crypti/crypti-docs/blob/master/install.md)
