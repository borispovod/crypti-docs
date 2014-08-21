# Crypti Boot2Docker installation

## 1. Install Boot2Docker

1. Browse to [Boot2Docker] (http://boot2docker.io)

2. Download Boot2Docker for your operating system

3. Install Boot2Docker default installation (with VirtualBox, MSYS git, etc...)


## 2. Run the Crypti Docker node and access web wallet

1. Launch Docker (if not running) via the desktop shortcut "Boot2Docker Start"

2. In the console window, type the following command:

        docker run -p 6040:6040 crypti/XXXX
    
3. The command will download the latest version of Crypti node from the Docker Hub, and launch it

4. Browse to [http://192.168.59.103:6040] (http://192.168.59.103:6040) in order to access the web wallet


## 3. Enable forging

**Note:** You need to have at least 1000 XCR in the account that you would like to forge with.

**Note2:** The account can be set only to a single node at a time, and any particular node can forge for a single account only.

1. Access the Crypti Docker container by connecting via SSH (user = ubuntu, password = XXXX):

        ssh 192.168.59.103

2. Change directory to src:

        cd src
         
3. Open config.json

        nano config.json

4. Navigate to the following section:

        "forging": {
            "secretPhrase" : ""
        }

5. Set the secretPhrase parameter to your account secret phrase.

6. Exit and save the file

        Ctrl-X, y

7. Restart Crypti node:

        forever restart app.js

8. Browse and login to the web wallet, navigate to "Forging" section, and verify that **Forging enabled** appears
in the top right corner.