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

### 2. Install Crypti

To install and run the latest version of Crypti - Delegate and Developer Edition, simply run the following command:

```
docker run -d --restart=always -p 0.0.0.0:8040:8040 cryptichain/node
```

**NOTE:** On Windows or Mac OS X, this command is issued from within the Docker Quickstart Terminal.

Upon successful completion, you will have a running Crypti node with an up-to-date snapshot of the blockchain. The container is configured to automatically restart upon reboot of the server or any occurrence of an error.

To access the Crypti web client, open: [http://server_ip:8040/](http://server_ip:8040/), replacing **server_ip** with your public IP address.

The Crypti web client should launch successfully.

### 3. Useful Commands

To see a list of running docker containers:

```
docker ps -a
```

To access a bash prompt on a docker container:

```
docker exec -it [container_id] /bin/bash
```

To monitor the status of a docker container:

```
docker stats [container_id]
```

To monitor the log file of a docker container:

```
docker logs -f [container_id]
```

To stop/restart/start a docker container:

```
docker stop [container_id]
docker restart [container_id]
docker start [container_id]
```

To view a full list of available commands:

```
docker --help
```

For further information on how to install or use Docker, please read the official [Docker Documentation](http://docs.docker.com/).
