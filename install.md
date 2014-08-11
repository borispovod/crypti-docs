Crypti Installation on Debian 7/Ubuntu 14

## 1. Install Node.js on Debian.

The current version of the node.js package is at:

[https://packages.debian.org/ru/wheezy-backports/nodejs](https://packages.debian.org/ru/wheezy-backports/nodejs)

Run: 

*sudo apt-get update*

To install, run:

*sudo apt-get install nodejs*

*sudo apt-get install nodejs-legacy*

On debian repositories must be found, on ubuntu if repositories not found:

Use this tutorial to add nodejs ppa repo:

[https://launchpad.net/~chris-lea/+archive/ubuntu/node.](https://launchpad.net/~chris-lea/+archive/ubuntu/node.js-legacy)*[js-legac*y](https://launchpad.net/~chris-lea/+archive/ubuntu/node.js-legacy)

Again update your system repositories and install nodejs:

*sudo apt-get update*

*sudo apt-get install nodejs*

After it installs, check version of node.js:

*node -v*

## 2. Install npm (Node package manager) on Debian.

Package:

[https://packages.debian.org/unstable/main/npm](https://packages.debian.org/unstable/main/npm)

To install run:

*sudo apt-get update*

*sudo apt-get install npm*

Check version of npm:

*npm -v*

## 3.  Install build-essential

*sudo apt-get install build-essential*

## 4. Install Crypti.

Upload Crypti archive to server.

Unzip it:

*sudo apt-get install unzip*

*unzip cryptibuilded.zip*

Go to crypti folder:

*cd cryptibuilded*

Run command:

*npm install*

In case you get ed25519 build errors, go to ed25519-node folder:

*cd ed25519-node*

And run:

*node-gyp configure*

And then:

*node-gyp build*

After it builds, go back to crypti folder and run the installation again:

*npm install*

## 5. Start Crypti

Install node.js process manager:

*sudo npm install -g forever*

And run crypti:

*forever start app.js*

Crypti process, logs, and etc can be found with the command:

*forever list*

You will see list of working nodejs process with logs and process ids, indexes.

Open the created log file:

*cat logs.log*

Verify that Crypti has started without any errors and synchronized with db.

After it starts,open: [http://serverip:6040/](http://serverip:6040/)

Crypti web wallet will be loaded.


## 6. Enable forging

Note: You need to have at least 1000 XCR in the account that you would like to forge with.

Note2: The account can be set only to a single node at a time, and any particular node can forge for a single account only.

Open config.json

Find the following section:

        "forging": {
            "secretPhrase" : ""
        }

Set the secretPhrase parameter to your account secret phrase.

Restart crypti:

*forever restart app.js*


Check in logs for message:

"Forging enabled"
 