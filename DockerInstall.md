# Installing Crypti using Docker

This tutorial describes how to install the Crypti - Delegate and Developer Edition, using a Docker based container.

## 1. Install Docker

### Windows / Mac OS X

1. Download and install [Docker Toolbox](https://www.docker.com/docker-toolbox) for your operating system.
2. Open the Docker Quickstart Terminal.

### Ubuntu

Log onto your Ubuntu based server and enter the following commands:

**NOTE:** The following is only applicable to: **Ubuntu 14.04 (LTS) - 64 bit**.

```
curl -sL http://downloads.cryptichain.me/setup_docker | sudo -E bash -
sudo apt-get install -y docker-engine
```

## 2. Install Crypti

To install and run the latest version of Crypti - Delegate and Developer Edition, simply run the following command:

```
sudo docker run -d --restart=always -p 0.0.0.0:8040:8040 cryptichain/node
```

**NOTE:** On Windows or Mac OS X, this command is issued from within the Docker Quickstart Terminal.

Upon successful completion, you will have a running Crypti node with an up-to-date snapshot of the blockchain. The container is configured to automatically restart upon reboot of the server or any occurrence of an error.

To access the Crypti web client, open: [http://server_ip:8040/](http://server_ip:8040/), replace **server_ip** with your public IP address.

The Crypti web client should launch successfully.

## 3. Enable Forging

**NOTE:** You may enable forging through the client or choose to have it automatically enabled every time the client is started. To have this process automated, follow the steps below.

Get the docker container id:

```
sudo docker ps -a
```

Open a bash prompt on the docker container (replace **[container_id]** with your own id):

```
sudo docker exec -it [container_id] /bin/bash
```

Open config.json:

```
export TERM=xterm; sudo nano config.json
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

Exit the docker container:

```
exit
```

Restart the docker container (replace **[container_id]** with your own id):

```
sudo docker restart [container_id]
```

Browse and login to the web client, navigate to "Forging" section, and verify that **Forging (Enabled)** appears in the top left corner.

## 4. Useful Commands

To see a list of running docker containers:

```
sudo docker ps -a
```

To access a bash prompt on a docker container:

```
sudo docker exec -it [container_id] /bin/bash
```

To monitor the status of a docker container:

```
sudo docker stats [container_id]
```

To monitor the log file of a docker container:

```
sudo docker logs --tail=500 -f [container_id]
```

To stop/restart/start a docker container:

```
sudo docker stop [container_id]
sudo docker restart [container_id]
sudo docker start [container_id]
```

To view a full list of available commands:

```
sudo docker --help
```

For further information on how to install or use Docker, please read the official [Docker Documentation](http://docs.docker.com/).
