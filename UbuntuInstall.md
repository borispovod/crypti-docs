# Installing Crypti on Ubuntu Linux

This tutorial describes how to install the Crypti - Delegate and Developer Edition, on a Ubuntu based server.

**NOTE:** The following is only applicable to: **Ubuntu 14.04 (LTS) - 64 bit**.

## 1. Install Essentials

```
sudo apt-get update
sudo apt-get install curl build-essential python wget unzip
```

## 2. Install SQLite3

```
curl -sL http://downloads.cryptichain.me/setup_sqlite3 | sudo -E bash -
sudo apt-get install -y sqlite3
```

After it installs, check version of sqlite3:

```
sqlite3 -version
```

SQLite3 should have the following version number: `3.8.2`

## 3. Install Node.js

```
curl -sL https://deb.nodesource.com/setup_0.12 | sudo -E bash -
sudo apt-get install -y nodejs
```

After it installs, check version of Node.js/npm:

```
node -v
npm -v
```

- Node.js should have the following version number: `v0.12.7`
- npm should have the following version number: `2.11.3`

## 4. Install Crypti

Download Crypti archive to server:

```
wget http://downloads.crypti.me/crypti-node/0.5.x/0.5.2.zip
```

Unzip the archive:

```
unzip 0.5.2.zip
```

Go to the Crypti folder:

```
cd 0.5.2
```

Run command:

```
npm install --production
```

## 5. Install Crypti Node

This is a specialized version of Node.js used to execute dapps within a virtual machine.

Download Crypti Node archive to server:

```
wget http://downloads.cryptichain.me/crypti-node.zip
```

Unzip the archive:

```
unzip crypti-node.zip
```

Check version of Node.js:

```
nodejs/node -v
```

- Node.js should have the following version number: `v0.12.2`

## 6. Download Blockchain

Download blockchain archive to server:

```
wget http://downloads.crypti.me/blockchain.db.zip
```

Unzip the archive:

```
unzip blockchain.db.zip
```

## 7. Start Crypti

Install forever, a Node.js process manager:

```
sudo npm install -g forever
```

Next synchronize your server clock:

```
sudo service ntp stop
sudo ntpdate pool.ntp.org
sudo service ntp start
```

**NOTE:** Some systems don't have ntp running so you may get the message "ntp: unrecognized service". This is ok just continue with next command.

Start Crypti:

```
forever start app.js
```

The Crypti process, logs, and etc can be found with the command:

```
forever list
```

You will see list of working Node.js processes with logs, process ids and indexes.

Verify that Crypti has started without any errors and synchronized with the db.

After it starts, open: [http://server_ip:8040/](http://server_ip:8040/), replace **server_ip** with your public IP address.

The Crypti web client should launch successfully.

## 8. Enable Forging

**NOTE:** You may enable forging through the client or choose to have it automatically enabled every time the client started. To have this process automated, follow the steps below.

Stop the running Crypti node:

```
forever stop app.js
```

Open config.json:

```
nano config.json
```

Arrow down until you find the following section:

```
"forging": {
  "secret" : [""]
}
```

Set the secret parameter to your account secret phrase.

```
"forging": {
  "secret" : ["YourDelegatePassphrase"] <- Replace with your delegate passphrase
}
```

In the forging section you will also see an access property, this is used to allow only your IP address to enable forging through the client.

```
"access": {
  "whiteList": ["127.0.0.1"] <- Replace with your IP which you will use to access your client
}
```

To set 2 accounts to forge on a single node, enter both account passphrases like below.

```
"forging": {
  "secret" : ["YourDelegatePassphrase1","YourDelegatePassphrase2"] <- Replace with your delegates passphrases
  "access": {
    "whiteList": ["127.0.0.1"]
  }
}
```

After you have typed in your passphrase. Hit: `Ctrl+ X` Then: `Y`

Restart Crypti:

```
forever restart app.js
```

Browse and login to the web client, navigate to "Forging" section, and verify that **Forging (Enabled)** appears in the top left corner.

## 9. Enable Secure Sockets Layer (SSL)

**NOTE:** To complete this step you require a signed certificate (from a CA) and a public and private key pair.

Stop the running Crypti node:

```
forever stop app.js
```

Open config.json:

```
nano config.json
```

Arrow down until you find the following section:

```
"ssl": {
  "enabled": false,         < Change FROM false TO true
  "options": {
    "port": 443,            < Default SSL Port
    "address": "0.0.0.0",   < Change only if you wish to block web access to the node
    "key": "path_to_key",   < Replace FROM path_to_key TO actual path to key file
    "cert": "path_to_cert"  < Replace FROM path_to_cert TO actual path to certificate file
  }
}
```

After you are done, save changes and exit. Hit: `Ctrl+ X` Then: `Y`

**NOTE:** If SSL Port configured above (ssl > options > port) is within well known ports range (below 1024), you must start Crypti using admin rights:

```
sudo forever start app.js
```

Else, if the port is above 1023, you can restart Crypti normally:

```
forever start app.js
```

Browse to the web client. You should now be able to use a secured connection.

## 10. Configure Autostart

To automatically launch Crypti each time your server restarts:

1. Install forever-service, a Linux tool which automatically launches Node.js scripts after a server restart.

  ```
  sudo npm install forever-service -g
  ```

2. Go to your Crypti folder and run:

  ```
  forever-service install crypti
  ```

3. Now you can start, stop and restart Crypti with the following commands.

  Start: ```sudo start crypti```

  Stop:  ```sudo stop crypti```

  Restart:  ```sudo restart crypti```

  Status:  ```sudo status crypti```

**NOTE:** By installing forever-service, you won't have to start Crypti with the command `sudo forever start app.js` anymore!

## 11. Troubleshooting

If it appears that *forever*, *nodejs* or *your home folder* has been deleted during an update process from an earlier Crypti version, the following errors can occur.

  * `bash: /usr/local/bin/forever: No such file or directory`
  * `npm ERR! cb() never called!`
  * `npm ERR! not ok code 0`

You have to make sure that your old Crypti client isn't running anymore. Then follow the these steps:

  1. Run `sudo apt-get clean`
  2. Run `sudo apt-get update`
  3. Follow the installation guide again (just don't re-install forever!)
  4. Run `sudo npm cache clear`
  5. Run `sudo npm install -g forever`

Your problem should now be resolved.
