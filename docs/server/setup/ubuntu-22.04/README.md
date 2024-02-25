
# Installation

## Docker

```bash
# Prepare APT for Docker Installation
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
apt-cache policy docker-ce
```

```bash
# Install Docker
sudo apt install docker-ce
# Verify its running
sudo systemctl status docker
# Grant user access to docker
sudo usermod -aG docker ${USER}
# Reload shell
su - ${USER}
# Verify we can access docker
docker ps
```
