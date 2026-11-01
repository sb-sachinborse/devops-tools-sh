# Devops Tools

### Jenkins

```
sudo apt update
sudo apt install fontconfig openjdk-21-jre
java -version
```
- Long Term Support release
```
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins

```

- Start Jenkins
You can enable the Jenkins service to start at boot with the command:
```
sudo systemctl enable jenkins
```
- You can start the Jenkins service with the command:
```
sudo systemctl start jenkins
```
- You can check the status of the Jenkins service using the command:
```
sudo systemctl status jenkins
```
```
Browse to http://localhost:8080 (or whichever port you configured for Jenkins when installing it) and wait until the Unlock Jenkins page appears.
```

<hr>

### Docker

##### quick setup

```
#install docker
suod apt install docker.io -y

# Add your current user to the docker group
sudo usermod -aG docker $USER

# Activate the group changes immediately in your current terminal session
newgrp docker


```

#### Install using the apt repository
- setup docker repository
```
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
```
- Install the Docker packages.

```
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
- After installation, verify that Docker is running:

```
sudo systemctl status docker
```
- If Docker is not running, start it manually:

```
sudo systemctl start docker

````
- verify docker
```
docker --version
```

## sonarqube using docker 
```
docker run -d --name sonarqube-scan -p 9000:9000 sonarqube:community
```

```
docker ps
```

```
#open sonarqube ui
http://<External ip>:9000
```

```
username and password : admin
```
<hr>

## Trivy
```
sudo apt-get install wget gnupg
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy
```

- verify installation
```
trivy --version
```
<hr>

# checkov

- Installing Checkov is quick and straightforward—just install, configure input, and scan.

- Install From PyPi Using Pip

```
pip install checkov

      #or
      
pip3 install checkov

```

<hr>

## prometheus

```
wget https://github.com/prometheus/prometheus/releases/download/v3.13.5/prometheus-3.13.5.linux-amd64.tar.gz
```
```
tar -xvf prometheus-3.13.5.linux-amd64.tar.gz
```


<hr>




















