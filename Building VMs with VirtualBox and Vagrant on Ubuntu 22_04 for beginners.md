## Building VMs with VirtualBox and Vagrant on Ubuntu 22_04 for beginners  
### Install VirtualBox and Vagrant
Update and upgrade the package index in Terminal: 
```
sudo apt update
```
Import VB package repositories keys:
```
Sudo apt install curl -y
curl https://www.virtualbox.org/download/oracle_vbox_2016.asc | gpg --dearmor > oracle_vbox_2016.gpg
curl https://www.virtualbox.org/download/oracle_vbox.asc | gpg --dearmor > oracle_vbox.gpg
sudo install -o root -g root -m 644 oracle_vbox_2016.gpg /etc/apt/trusted.gpg.d/</p>
sudo install -o root -g root -m 644 oracle_vbox.gpg /etc/apt/trusted.gpg.d/</p>
```
Add the VirtualBox repository:
```
echo "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian $(lsb_release -sc) contrib" | sudo tee /etc/apt/sources.list.d/virtualbox.list
```
Install VirtualBox-6.1 (check if it appears on your computer):
```
sudo apt update
sudo apt install -y linux-headers-$(uname -r) dkms
sudo apt install virtualbox-6.1 -y
```
Install Vagrant:
```
sudo apt install vagrant -y
```
Check Vagrant version:
```
vagrant --version
```
### Creating a virtual machine
Create a Vagrant file:
```
Make a new directory for yours virtual machines called u22 (where you will create the Vagrant files):
```
mkdir u22
```
Gate into u22 (command *cd* is for to go into this directory):
```
cd u22
```
Check you are in the path  */u22$*: (comand *pwd* = print working directory):
```
pwd
```
vagrant init
```
### Setting a Static IP address to your virtual machine:
Open VirtualBox
In the Host Menu / Network / Create 
Take note of your VirtualBox Host IP address.

![virtualbox_host_network_create](https://github.com/DoriCastilla/Eramba-virtual-machine/assets/170856411/0b2e3b88-4eba-4f59-9c49-c3e695b21d84)

Going back to Terminal, you are going to change the IP of your virtual machine. Remember you must be in the u22 directory:
```
nano Vagrantfile
```
Look for the row  **# config.vm.network = “base”**, delete it and paste this (remember to remove the # too): <br>
```
config.vm.box = "bento/ubuntu-22.04"
```
Look for the row **# config.vm.network “private network”,  ip: “192.168.x.y”** <br>
Change the 3rt octet, *x*, for 3rt octeto of your Virtualbox Host IP<br>
Change the 4th octet, *y*, for a random number above 1 and below 255.<br>
To exit: **Ctrl+X** <br>
Save modified buffer? **Y**<br>
<br>
Starts and provisions the vagrant environment:
```
vagrant up
```
### Connect your VM with the host
In Virtualbox start your virtual machine named u22.default_xxxx...<br>

<br> 
In u22-default_xxxx… open Setting/Network<br> 
Adapter 1: Enabled<br> 
Attached to: Bridget Adapter

![virtualbox_vm_network_adapter1](https://github.com/DoriCastilla/Eramba-virtual-machine/assets/170856411/b6f35ccf-8774-4aff-a23d-51d86784dead)
<br>
Adapter 2: Enable it<br>
Attached to: Host-only Adapter<br>
Save changes with OK

![virtualbox_vm_network_adapter2](https://github.com/DoriCastilla/Eramba-virtual-machine/assets/170856411/d4c657a0-01d3-4b2f-a419-6d5e05ffbeaf)
<br>

### Start the virtual machine and login <br>
Login: vagrant<br>
password: vagrant<br>
<br>
and check it has wireless internet connexion:
```
Ping 8.8.8.8
```





