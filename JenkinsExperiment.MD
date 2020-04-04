#### JENKINS PIPELINE Experiment:

##### SetUp Jenkins on Ubuntu:
```
sudo apt update
sudo apt install openjdk-8-jdk
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins
systemctl status jenkins
sudo ufw allow 8080
sudo ufw status
http://<your_ip>:8080


```
![image](https://user-images.githubusercontent.com/45539698/78454822-1c5ae380-76b8-11ea-9546-9f260b3c9db5.png)
![image](https://user-images.githubusercontent.com/45539698/78454948-0d286580-76b9-11ea-9d2d-f2619e47eebf.png)
