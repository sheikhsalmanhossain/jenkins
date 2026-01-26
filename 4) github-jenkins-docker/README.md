# Installing Jenkins in ec2 (ubuntu):

In security group add inbound rules port 8080, hence jenkins is running in this port.

In ec2 terminal run these commands to install java :

``` sudo apt update && sudo apt upgrade -y ```

``` sudo apt install -y fontconfig openjdk-17-jre ```

``` java -version ```



### Install Jenkins via SNAP :

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
