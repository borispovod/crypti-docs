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

To install and run the latest version of Crypti - Delegate and Developer Edition, simply run the following commands:

Download the latest docker image:

```
docker pull cryptichain/node
```

Install the docker image (executed only once per installation):

```
docker run -d --restart=always -p 0.0.0.0:8040:8040 cryptichain/node
```

**NOTE:** On Windows or Mac OS X, these commands are issued from within the Docker Quickstart Terminal.

Upon successful completion, you will have a running Crypti node with an up-to-date snapshot of the blockchain. The container is configured to automatically restart upon reboot of the server or any occurrence of an error.

To access the Crypti web client, open: [http://server_ip:8040/](http://server_ip:8040/), replace **server_ip** with your public IP address.

The Crypti web client should launch successfully.

## 3. Update Crypti

To update to the latest version of Crypti - Delegate and Developer Edition, simply run the following commands:

**WARNING:** The provided instructions will **remove the previous container** and **create a new one**. Please be sure to backup any data before proceeding. See: `docker cp --help` for more information on how to copy files from the container to the host machine.

Get the docker container id:

```
docker ps -a
```

Stop the docker container (replace **container_id** with your own id):

```
docker stop container_id
```

Remove the old container (replace **container_id** with your own id):

```
docker rm container_id
```

Download the latest docker image:

```
docker pull cryptichain/node
```

Install the docker image (executed only once per installation):

```
docker run -d --restart=always -p 0.0.0.0:8040:8040 cryptichain/node
```

Remove any dangling images:

```
docker rmi $(docker images -q --filter "dangling=true")
```

Your docker image should now be updated.

## 4. Enable Forging

**NOTE:** You may enable forging through the client or choose to have it automatically enabled every time the client is started. To have this process automated, follow the steps below.

Get the docker container id:

```
docker ps -a
```

Open a bash prompt on the docker container (replace **container_id** with your own id):

```
docker exec -it container_id bash
```

Open config.json:

```
export TERM=xterm; nano config.json
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

Restart the docker container (replace **container_id** with your own id):

```
docker restart container_id
```

Browse and login to the web client, navigate to "Forging" section, and verify that **Forging (Enabled)** appears in the top left corner.

## 5. Enable Secure Sockets Layer (SSL)

**NOTE:** To complete this step you require a signed certificate (from a CA) and a public and private key pair.

Get the docker container id:

```
docker ps -a
```

Open a bash prompt on the docker container (replace **container_id** with your own id):

```
docker exec -it container_id bash
```

Open config.json:

```
export TERM=xterm; nano config.json
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

Exit the docker container:

```
exit
```

Stop the docker container (replace **container_id** with your own id):

```
docker stop container_id
```

Commit a new docker image (replace **container_id** with your own id):

```
docker commit container_id secure_node
```

Run the new docker image:

```
docker run -d --restart=always -p 0.0.0.0:8040:8040 0.0.0.0:443:443 secure_node
```

Browse to the web client. You should now be able to use a secured connection.

## 6. Useful Commands

To see a list of running docker containers:

```
docker ps -a
```

To access a bash prompt on a docker container:

```
docker exec -it container_id bash
```

To monitor the status of a docker container:

```
docker stats container_id
```

To monitor the log file of a docker container:

```
docker logs --tail=500 -f container_id
```

To stop/restart/start a docker container:

```
docker stop container_id
docker restart container_id
docker start container_id
```

To view a full list of available commands:

```
docker --help
```

For further information on how to install or use Docker, please read the official [Docker Documentation](http://docs.docker.com/).

## 7. Troubleshooting

If you encounter the following error when running `docker` commands:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Then please try running each command prefixed with `sudo`. For example: `sudo docker ps -a`.

If this does not work, please check the Docker daemon is running correctly before proceeding.

***

If you encounter an error while downloading the docker image, using the `docker pull` command.

Please use the following alternative download method:

```
curl -o docker_image.tar.gz http://downloads.cryptichain.me/docker_image.tar.gz
zcat docker_image.tar.gz | docker load
```

Then proceed with the remainder of the [installation instructions](DockerInstall.md#2-install-crypti).
