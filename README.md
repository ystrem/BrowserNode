# BrowserNode
- Projects which I run is in [DePinProjects](https://github.com/ystrem/BrowserNode/blob/main/DePinProjects.md)

# Extension-nodes

Installing Chromium browser to run the extension depin nodes

---

# Join Community

Join TG : [Crypto Chihuahua Telegram](https://t.me/+06vAiua6sWBhNzRk) 

Follow X : (https://www.x.com/ystrem) 

---

## Hardware requirements:


- Something like Cloud VPS 4C from Contabo should be fine.


Here’s an alternative method to install and run Chromium using Docker, based on the `lscr.io/linuxserver/chromium:latest` image:

###  1: Update VPS
```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo apt install curl -y
sudo apt install ca-certificates
```

###  2: Install Docker
```
https://docs.docker.com/engine/install/ubuntu/

or

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
docker version
```
###  3: Install docker compose
```
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)

curl -L "https://github.com/docker/compose/releases/download/"$VER"/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

### 4. Create a Project Directory:
```bash
mkdir chromium
cd chromium
```

### 5. Create a `docker-compose.yml` File:
```bash
nano docker-compose.yml
```

### 6. Paste This Docker Compose Configuration:

```yaml
---
services:
  chromium:
    image: lscr.io/linuxserver/chromium:latest
    container_name: chromium
    security_opt:
      - seccomp:unconfined #optional
    environment:
      - CUSTOM_USER= #Replace username
      - PASSWORD= #Replace password
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - CHROME_CLI=https://github.com/0xmoei #optional
    volumes:
      - /root/chromium/config:/config
    ports:
#      - 3010:3000   # HTTP not secure disabled 
      - 3011:3001   # HTTPS 
    shm_size: "4gb"
    restart: unless-stopped
```

### 7. Save and Exit:
Save the file by pressing `Ctrl + X`, then `Y`, and press `Enter`.

### 8. Start the Container:
Run the following command to spin up the Chromium container:
```bash
docker-compose up -d
```

### 9. Access Chromium:
Open your browser and visit:

https://<VPS_IP>:3011

You can now access Chromium remotely via the VNC interface with your set username and password.
