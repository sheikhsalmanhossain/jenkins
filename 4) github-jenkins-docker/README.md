## Installing Jenkins in ec2 (ubuntu):

In security group add inbound rules port 8080, hence jenkins is running in this port.

In ec2 terminal run these commands to install java :

``` sudo apt update && sudo apt upgrade -y ```

``` sudo apt install -y fontconfig openjdk-17-jre ```

``` java -version ```



#### Install Jenkins via SNAP :

```
sudo apt update
sudo apt install -y snapd
```
Install Jenkins :

``` sudo snap install jenkins --classic ```

Start Jenkins :
```
sudo systemctl enable snap.jenkins.daemon
sudo systemctl start snap.jenkins.daemon
```
check if snapd is running :
``` systemctl status snapd ```

If it’s not active, start it:
```
sudo systemctl enable snapd
sudo systemctl start snapd
```

Verify snap works :

``` snap version ```

If this fails, log out and log back in, or reboot once:

``` sudo reboot ```

Check Jenkins snap services :

``` snap services Jenkins ```

Start Jenkins 

``` sudo snap start Jenkins ```

Browse jenkins :

``` ip:8080 ```



## Installing docker on ec2 ubuntu 24.04 :

``` sudo apt update && sudo apt upgrade -y ```

Install required dependencies:

``` sudo apt install -y ca-certificates curl gnupg lsb-release ```

Add Docker’s official GPG key :

```
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
  | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

Set correct permissions:
``` sudo chmod a+r /etc/apt/keyrings/docker.gpg ```

Add the Docker repository :

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" \
| sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Install Docker Engine :

```
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Verify Docker is running :

``` sudo systemctl status docker ```









### Add Jenkins to docker group :
Hence we install Jenkins via "snap", it does NOT create a jenkins Linux user.Snap Jenkins runs confined and uses snap permissions, not a system user.


Allow Jenkins snap to access Docker :
```
sudo snap connect jenkins:docker
sudo snap connect jenkins:docker-executables
```
Add current user to Docker group :
``` sudo usermod -aG docker ubuntu ```

then ``` logout ```

Restart Docker & Jenkins :
```
sudo systemctl restart docker
sudo snap restart Jenkins
```
Verify Docker works ``` docker ps ```


( Snap Jenkins is not ideal for Docker-heavy CI.
Instead Install Jenkins via apt, Or Run Jenkins inside Docker) 
