# Crypti Boot2Docker installation

## 1. Install Boot2Docker

1. Browse to [Boot2Docker] (http://boot2docker.io)

2. Download Boot2Docker for your operating system

3. Install Boot2Docker default installation (with VirtualBox, MSYS git, etc...)


## 2. Run the Crypti Docker node and access web wallet

1. Launch Docker (if not running) via the desktop shortcut "Boot2Docker Start"

2. In the console window, type the following command:

        docker run -d -p 6040:6040 crypti/node
    
3. The command will download the latest version of Crypti node from the Docker Hub, and launch it

4. Browse to [http://192.168.59.103:6040] (http://192.168.59.103:6040) in order to access the web wallet


## 3. Enable forging

**Note:** You need to have at least 1000 XCR in the account that you would like to forge with.

**Note2:** The account can be set only to a single node at a time, and any particular node can forge for a single account only.

1. Stop the running Docker image (if running):

        docker ps
        docker stop CONTAINER_ID <--- The ID returned by docker ps

2. Set the forging password via sed:

        docker run crypti/node sed -i 's/""/"PASSWORD"/g' src/config.json
         
3. Save the change in a new Docker container:

        docker ps -l
        docker commit CONTAINER_ID my/forger <--- The ID returned by docker ps -l

3. Verify that correct password is set correctly, by looking at the "secretPhrase" at the end of config:

        docker run my/forger cat src/config.json

4. Start the forging node:

        docker run -d -p 6040:6040 my/forger forever /src/app.js

8. Browse and login to the web wallet, navigate to "Forging" section, and verify that **Forging enabled** appears
in the top right corner.