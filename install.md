# Crypti Installation on Debian 7 / Ubuntu 14

## 1. Install Node.js

The current version of the node.js package is [here](https://packages.debian.org/ru/wheezy-backports/nodejs)

Run: 

    sudo apt-get update

To install, run:

    sudo apt-get install nodejs

    sudo apt-get install nodejs-legacy

On debian repositories must be found, on ubuntu if repositories not found:

You must add the [nodejs ppa repo:](https://launchpad.net/~chris-lea/+archive/ubuntu/node.js-legacy)
Use this command

    sudo apt-add-repository ppa:chris-lea/node.js-legacy

Again update your system repositories and install nodejs/sqlite3:

    sudo apt-get update

    sudo apt-get install nodejs
    
    sudo apt-get install sqlite3

After it installs, check version of node.js/sqlite3:

    node -v
    sqlite3 -v

## 2. Install npm (Node package manager)

[Package:](https://packages.debian.org/unstable/main/npm)

To install run:

    sudo apt-get update
    
Then:
   

     sudo apt-get install npm

Check version of npm:

    npm -v

## 3.  Install build-essential

    sudo apt-get install build-essential

## 4. Install Crypti.

Download Crypti archive to server:

    wget http://downloads.crypti.me/crypti-node/0.3.x/0.3.x.zip

Install unzip:

    sudo apt-get install unzip

Unzip it:
   

     unzip 0.3.x.zip

Go to crypti folder:

    cd 0.3.x

Run command:

    npm install --production


## 5. Start Crypti

Install node.js process manager:

    sudo npm install -g forever
 
 Next synchronize your server clock :

    sudo service ntp stop
    sudo ntpdate pool.ntp.org
    sudo service ntp start
**Note:** Some systems don't have ntp running so you may get the message "ntp: unrecognized service" This is ok just continue with next command

And run crypti:

    forever start app.js

Crypti process, logs, and etc can be found with the command:

    forever list

You will see list of working nodejs process with logs and process ids, indexes.

Verify that Crypti has started without any errors and synchronized with db.

After it starts,open: [http://serverip:8040/](http://serverip:8040/) <--- Replace "serverip" with Your **Public IP**

Crypti web wallet will be loaded.


## 6. Enable forging

**Note:** You may enable forging through the wallet or choose to have it automatically enable foring everytime the wallet is started. To have this process automated, follow the steps below.


Stop the running Crypti node

    forever stop app.js

Open config.json

    sudo nano config.json

Arrow down untill you find the following section:

        "forging": {
          "secret" : [""]
        }

Set the secret parameter to your account secret phrase.

       "forging": {
         "secret" : ["YourWalletPassphrase"]  <- Replace With your wallets passphrase

In the forging section you will also see an Access line, this is used to allow only your IP access to enable forging through the wallet.

       "access": {
                        "whiteList": ["127.0.0.1"]  <- Replace With your IP which you will use to access your wallet

To set 2 accounts to forge on a single node, enter both account passphrases like below.

       "forging": {
         "secret" : ["YourWalletPassphrase1","YourWalletPassphrase2"]  <- Replace With your wallets passphrase
         "access": {
                        "whiteList": ["127.0.0.1"]
	}
After you type in your Passphrase Hit:

    Ctrl+ X
Then: 

    Y 

Restart crypti:

    forever start app.js

Browse and login to the web wallet, navigate to "Forging" section, and verify that **Stop Forging** appears
in the top right corner. This shows that you are already forging.

## 7. Enable Secure Sockets Layer (SSL)

**Note:** To complete this step you require a signed certificate (by a CA)  and a public and private key pair

Stop the running Crypti node

    forever stop app.js

Open config.json

    sudo nano config.json

Arrow down untill you find the following section:

	"ssl": {
		"enabled": false,   < Change FROM false TO true
		"options": {
			"port": 443,    < Default SSL Port    
			"address": "0.0.0.0",   < Change only if you wish to block web access to the node	
			"key": "path_to_key",   < Replace FROM path_to_key TO actual path to key file
			"cert": "path_to_cert"  < Replace FROM path_to_cert TO actual path to certificate file
		}
	}

After you are done, save changes and exit: 

    Ctrl+ X
    
Then confirm saving: 

    Y 

**Note:** If SSL Port configured above (ssl > options > port) is within well known ports range (below 1024), you must start crypti using admin rights:

    sudo forever start app.js
    
Else, if port is above 1023, you restart crypti regulary:

    forever start app.js

Browse to the web wallet. You should now be able to use a secured connection 

# Autostart

To automatically launch crypti each time your server restarts:

1. Edit your crontab file (replacing ```<user>``` with your own).

  ```crontab -u <user> -e```

2. Select an editor to open your crontab file with.

  ```
  Select an editor. To change later, run 'select-editor'.
    1. /bin/ed
    2. /bin/nano    <---- easiest
  ```

  Choose nano (option 2) and and press enter to continue.

3. Append the following text to your crontab file.

  ```@reboot <forever_path> start <crypti_path>/app.js```

  1. Replace ```<forever_path>``` with the path to the forever command on your system.  
  For example: ```/usr/bin/forever``` on Ubuntu/Debian based operating systems.
  
  2. Replace ```<crypti_path>``` with your crypti installation path. For example: ```/home/user/crypti```.

4. Save your crontab file by pressing ```ctrl+o``` and ```ctrl+x``` to exit.

5. Reload cron for your changes to take effect (replacing ```<user>``` with your own).

  ```crontab -u <user> -l```
