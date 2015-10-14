# Crypti Installation on Debian 7 / Ubuntu 14

## 1.  Install Build Essentials

    sudo apt-get update
    sudo apt-get install build-essential

## 2.  Install SQLite

    sudo apt-get install sqlite3

After it installs, check version of sqlite3:

    sqlite3 -version

Sqlite3 should have the following version number:

- `3.7.13` on Debian 7
- `3.8.2` on Ubuntu 14

## 3. Install Node.js

After it installs, check version of node.js/npm:

    node -v
    npm -v

- Nodejs should have the following version number: ```v0.10.40``` 
- Npm should have the following version number: ```1.4.28```

## 4. Install Crypti

Download Crypti archive to server:

    wget http://downloads.crypti.me/crypti-node/0.3.x/0.3.2.zip

Install unzip:

    sudo apt-get install unzip

Unzip it:
   
     unzip 0.3.2.zip

Go to the Crypti folder:

    cd 0.3.2

Run command:

    npm install --production

## 5. Start Crypti

Install node.js process manager:

    sudo npm install -g forever
 
Next synchronize your server clock:

    sudo service ntp stop
    sudo ntpdate pool.ntp.org
    sudo service ntp start
    
**Note:** Some systems don't have ntp running so you may get the message "ntp: unrecognized service". This is ok just continue with next command. 

And run Crypti:

    forever start app.js

Crypti process, logs, and etc can be found with the command:

    forever list

You will see list of working nodejs process with logs and process ids, indexes.

Verify that Crypti has started without any errors and synchronized with db.

After it starts, open: [http://serverip:8040/](http://serverip:8040/) <--- Replace "serverip" with Your **Public IP**

Crypti web client will be loaded.

## 6. Enable Forging

**Note:** You may enable forging through the client or choose to have it automatically enable forging everytime the client started. To have this process automated, follow the steps below.

Stop the running Crypti node:

    forever stop app.js

Open config.json:

    sudo nano config.json

Arrow down untill you find the following section:

        "forging": {
          "secret" : [""]
        }

Set the secret parameter to your account secret phrase.

       "forging": {
         "secret" : ["YourDelegatePassphrase"]  <- Replace with your delegate passphrase

In the forging section you will also see an access line, this is used to allow only your IP address to enable forging through the client.

       "access": {
                        "whiteList": ["127.0.0.1"]  <- Replace with your IP which you will use to access your client

To set 2 accounts to forge on a single node, enter both account passphrases like below.

       "forging": {
         "secret" : ["YourDelegatePassphrase1","YourDelegatePassphrase2"]  <- Replace with your delegates passphrases
         "access": {
                        "whiteList": ["127.0.0.1"]
	}
After you type in your Passphrase Hit:

    Ctrl+ X
    
Then: 

    Y 

Restart Crypti:

    forever start app.js

Browse and login to the web client, navigate to "Forging" section, and verify that **Stop Forging** appears
in the top right corner. This shows that you are already forging.

## 7. Enable Secure Sockets Layer (SSL)

**Note:** To complete this step you require a signed certificate (by a CA)  and a public and private key pair.

Stop the running Crypti node:

    forever stop app.js

Open config.json:

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

**Note:** If SSL Port configured above (ssl > options > port) is within well known ports range (below 1024), you must start Crypti using admin rights:

    sudo forever start app.js
    
Else, if port is above 1023, you restart Crypti regulary:

    forever start app.js

Browse to the web client. You should now be able to use a secured connection.

# Autostart

To automatically launch Crypti each time your server restarts:

1. Install forever-service, a Linux tool which automatically launches Node.js scripts after a server restart. 

  ```sudo npm install forever-service -g```

2. Go to your Crypti folder and run:

  ```forever-service install crypti```

3. Now you can start, stop and restart Crypti with the following commands. 

    Start:  ```sudo start crypti```

    Stop:  ```sudo stop crypti```

    Restart:  ```sudo restart crypti```

    Get the status of the forever process:  ```sudo status crypti```

**Note:** If you install forever-service and want to use it, you don't have to start Crypti with the command ```sudo forever start app.js``` anymore!

# Troubleshooting

If it appears that *forever*, *nodejs* or *your home folder* has been deleted during an update process from an earlier Crypti version, the following errors can occur. 

* ```bash: /usr/local/bin/forever: No such file or directory```
* ```npm ERR! cb() never called!```
* ```npm ERR! not ok code 0```

You have to make sure that your old Crypti client isn't running anymore. Then follow the these steps:

  1. Run ```sudo apt-get clean```
  2. Run ```sudo apt-get update```
  3. Follow the installation guide again (just don't re-install forever!)
  4. Run ```sudo npm cache clear```
  5. Run ```sudo npm install -g forever```

Your problem should be fixed now.
