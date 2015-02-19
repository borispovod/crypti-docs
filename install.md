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

    wget http://downloads.crypti.me/crypti-node/0.1.x/0.1.9b.zip

Install unzip:

    sudo apt-get install unzip

Unzip it:
   

     unzip 0.1.9b.zip

Go to crypti folder:

    cd 0.1.9b

Run command:

    npm install

Then:

    cd node_modules


Then:

    cd ed25519

And run:

    node-gyp configure

And then:

    node-gyp build

After it builds, go back to crypti folder and run the installation again:

    cd

then: 

    cd 0.1.9b
Run:

    npm install

## 5. Start Crypti

Install node.js process manager:

    sudo npm install -g forever
    
Then if you would like use a recent official Crypti block-chain snapshot use this:

    wget http://downloads.crypti.me/blockchains/blockchain.db.zip
    
Unzip it:
   

     unzip blockchain.db.zip

And run crypti:

    forever start app.js

Crypti process, logs, and etc can be found with the command:

    forever list

You will see list of working nodejs process with logs and process ids, indexes.

Open the created log file:

    cat logs.log

Verify that Crypti has started without any errors and synchronized with db.

After it starts,open: [http://serverip:6040/](http://serverip:6040/) <--- Replace "serverip" with Your **Public IP**

Crypti web wallet will be loaded.


## 6. Enable forging

**Note:** You need to have at least 1000 XCR in the account that you would like to forge with.

**Note2:** The account can be set only to a single node at a time, and any particular node can forge for a single account only.

Stop the running Crypti node

    forever stop app.js

Open config.json

    sudo nano config.json

Arrow down untill you find the following section:

        "forging": {
          "secretPhrase" : ""
        }

Set the secretPhrase parameter to your account secret phrase.

       "forging": {
         "secretPhrase" : "YourWalletPassphrase"  <- Replace With your wallets passphrase
        }
After you type in your Passphrase Hit:

    Ctrl+ X
Then: 

    Y 

Restart crypti:

    forever start app.js

Browse and login to the web wallet, navigate to "Forging" section, and verify that **Forging enabled** appears
in the top right corner.
