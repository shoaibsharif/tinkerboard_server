# How to Create a cloud server With NextCloud and LAMP Stack Web Server 

### Before Reading
I am not an expert. This is not finished yet. There are something I still couldn't figure out. I am just trying by myself. I have searched a lot but didn't found a single information how to do it. I didn't found much resource for Tinkerboard, but there is a lot of resource for Raspberry Pi. I chose Tinkerboard because of its extended RAM and CPU. I will update if I discover anything.

## Choosing OS
I have chosen [Armbian Stretch](https://www.armbian.com/tinkerboard/) which is a very lightweight OS and a debian based linux system. Since I am going to use a headless server, I strongly recommend this OS. I always had issue with TinkerOS. I don't why everytime I tried to update my distro it gives me issues. I like its `armbian config` where you can just simply type `sudo armbian-config`and you can easily configure from the terminal. For more infor you can visit [Armbian Doc](https://docs.armbian.com/) to get started.

## Webmin
Then I actually wanted to instal Webmin. Webmin is a dashboard where you can configurey things for your server such as file manager, editing samba file sharing system, monitoring your system and make your life very easier. The installation process are [here](http://www.webmin.com/deb.html) and see **Using the Webmin APT repository**
But I have had an issue when installing its dependency `apt-get-versions`. When I tried to install I got this error:
```
** initializing cache. This may take a while **
Error: No information about packages! (Maybe no deb entries?)
dpkg: error processing package apt-show-versions (--configure):
 subprocess installed post-installation script returned error exit status 255
Errors were encountered while processing:
 apt-show-versions
E: Sub-process /usr/bin/dpkg returned an error code (1)

```
Then I found the solution from [this link] (https://askubuntu.com/questions/916199/install-apt-show-versions-inside-an-ubuntu-docker-container)
All you just have to do the following.(#):

```
# rm /etc/apt/apt.conf.d/docker-gzip-indexes
# apt-get purge apt-show-versions
# rm /var/lib/apt/lists/*lz4
# apt-get -o Acquire::GzipIndexes=false update

```
After that I tried to install `apt-show-versions` by the following command:
```
# apt-get install apt-show-versions
```
Then All you just have to type `your_ip:10000` and sign in with your username and password that has **root previliges**.

## NextCloud
I find installing NextCloudPi easier that installing NextCloud manually. When I run the following command:
```
# curl -sSL https://raw.githubusercontent.com/nextcloud/nextcloudpi/master/install.sh | bash
```
This will install LAMP stack and automatically configure the process but I don't know if it right or not because I also want to use this server as a web server too. So its tempting. I am still gonna use this.

