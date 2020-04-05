### Jenkins Pipeline:

#### SetUp Jenkins on Ubuntu:
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
![image](https://user-images.githubusercontent.com/45539698/78455099-f59dac80-76b9-11ea-8b92-2322167cb1cd.png)
![image](https://user-images.githubusercontent.com/45539698/78455259-da7f6c80-76ba-11ea-8dd2-16c501facfaa.png)
![image](https://user-images.githubusercontent.com/45539698/78455275-f3881d80-76ba-11ea-8556-8ed1e305c4f2.png)
![image](https://user-images.githubusercontent.com/45539698/78455311-334f0500-76bb-11ea-8061-17bebf22de1a.png)
#### Click on New Item:
![image](https://user-images.githubusercontent.com/45539698/78455387-bb350f00-76bb-11ea-96f6-656eb9c2bbec.png)
#### Create a Multibranch Pipeline:
![image](https://user-images.githubusercontent.com/45539698/78455496-5fb75100-76bc-11ea-8642-a01b1e9a3f1d.png)
#### Configure Github Credentails:
![image](https://user-images.githubusercontent.com/45539698/78455512-78c00200-76bc-11ea-9ce3-a62660393241.png)
#### Use this Github Credentails in the Multibranch Pipeline:
![image](https://user-images.githubusercontent.com/45539698/78455682-701bfb80-76bd-11ea-93bf-6ab3b65cda8a.png)
#### Set JDK | Maven configurations on Global Level:
![image](https://user-images.githubusercontent.com/45539698/78469007-78664c00-773a-11ea-9137-563f48052083.png)
![image](https://user-images.githubusercontent.com/45539698/78469017-8f0ca300-773a-11ea-9cc4-9717be6baa9f.png)

