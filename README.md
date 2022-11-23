# Minima
Minima Node Installation Instructions

## General information

### Official documentation:
```
https://docs.minima.global/docs/runanode/selectplatform/linux_vps/
```
### System requirements:
1 cpu, 
1 ram, 
20Gb ssd,
Ubuntu 20.04

### Before starting the installation, register a Minima account:
```
https://incentive.minima.global/account/register
```
# Installing the Minima Node
### 1. System update, environment installation:
```
apt update && apt dist-upgrade -y
```
```
apt install curl screen nmon htop -y
```
### 2. Create user minima:
```
sudo adduser minima9001
```
### 3. Let's give sudo rights to the created user:
```
sudo usermod -aG sudo minima9001
```
### 4. Let's connect under the minima user:
```
su - minima9001
```
### 5. Downloading the setup script:
```
sudo curl -fsSL https://get.docker.com/ -o get-docker.sh
```
### 6. Distribute the rights to run the script and execute the docker installation script:
```
sudo chmod +x ./get-docker.sh && ./get-docker.sh
```
### 7. Add a user to the docker group:
```
sudo usermod -aG docker minima9001
```
### 8. Output to apply docker management rights:
```
exit
```
### 9. Let's connect under the minima user:
```
su - minima9001
```
### 10. We set the password mds (instead of 123 in the command) and execute the command to create a container for the Minima node.
The password must consist of numbers and letters in lower case, without special characters!
```
docker run -d -e minima_mdspassword=123 -e minima_server=true -v ~/minimadocker9001:/home/minima/data -p 9001-9004:9001-9004 --restart unless-stopped --name minima9001 minimaglobal/minima:latest
```
### 11. We exit after the creation of the container is completed:
```
exit
```
### 12. We start services:
```
sudo systemctl enable docker.service
```
```
sudo systemctl enable containerd.service
```
### 13. Let's connect under the minima user:
```
su - minima9001
```
### 14. To set up automatic updates, install WATCHTOWER:
```
docker run -d --restart unless-stopped --name watchtower -e WATCHTOWER_CLEANUP=true -e WATCHTOWER_TIMEOUT=60s -v /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower
```
### 15. Checking minim containers:
```
docker ps
```
### 16. Open the browser and paste in Url https://YourServerIP:9003/ where change YourServerIP to your IP Address. We log in using the password that was set for mds.
If you do not know your IP, you can check it with the command:
```
wget -qO- eth0.me
```
### 17. We look for and open the Incentive Program minidapp, copy our Incentive ID there.
Incentive ID you can get on the page:
```
https://incentive.minima.global/home/pages/incentiveid
```
### 18. Check Rewards balance the next day (+1 every day)

# Additional Information
If you can't connect to the node using https://ip:9003 then you can register Incentive ID through the Minima terminal.
```
docker exec -it minima9001 /bin/sh
```
```
sh /bin/minima
```
Basic commands:

help - show all commands

mds - see password

status - view the status of your node

incentivecash - check balance

incentivecash uid: - bind node id

