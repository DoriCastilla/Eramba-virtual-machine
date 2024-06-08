## Establish and config an Eramba VM with static IP in VMware Workstation using Putty.

### Programs and files used:
Running and functioning:
- VMware Workstation 15 Pro
- Putty

Download Eramba OVF to your local computer, you need to fetch 3 files:
1.	[https://downloadseramba.s3.eu-west-1.amazonaws.com/CommunityVM/3181/eramba-disk1.vmdk](https://downloadseramba.s3.eu-west-1.amazonaws.com/CommunityVM/3181/eramba-disk1.vmdk)
2.	[https://downloadseramba.s3.eu-west-1.amazonaws.com/CommunityVM/3181/eramba.ovf](https://downloadseramba.s3.eu-west-1.amazonaws.com/CommunityVM/3181/eramba.ovf)
3.	[https://downloadseramba.s3.eu-west-1.amazonaws.com/CommunityVM/3181/eramba.mf](https://downloadseramba.s3.eu-west-1.amazonaws.com/CommunityVM/3181/eramba.mf)


### Installing Eramba: 
Start VMware workstation, 
- In the menu: File/Open 
- navigate to where you placed the downloaded Eramba files and select *eramba*, and press *Open*

Import the Eramba OVA.
- Give the vmguest a name. Here I did name it: “eramba-test-01”
- Specify there the new guest shall be stored
- Select *Import*

Power on this virtual machine when it is done.<br>
![eramba vm especifications](https://github.com/DoriCastilla/Eramba-virtual-machine/assets/170856411/dcb795f9-f5ea-42f3-be26-be1555ba8e82)

Login to VMguest eramba-test-01 by the console and after a litle while it will ask you for login.
Login username: eramba
Login password: eramba 
<sub>Hint about Workstation, you can get “locked” in to the console to get out, press: Alt+Ctrl</sub>

Successful login will show you few important things:
- Your eramba instance IP address: 192.168.140.129
- The interface the IP address is attached to: ens33

In this case the IP address is: 192.168.140.129  but yours might very well be different, and change from time to time, because stil lit is a dinamyc IP.  
Make a note of: 
- IP address: in this case 192.168.140.129
- Name of interface: in this case ens33<br>
 ![eramba_console_presentation](https://github.com/DoriCastilla/Eramba-virtual-machine/assets/170856411/9d946e5b-c300-43d1-bb12-4962a6ebde3c)

Verify that your new Eramba vmguest got Internet connectivity writting in the console: 
```
ping 8.8.8.8
```
<sub>Ctrol+C to stop it.</sub>

### Set a Static IP address in your eramba VMguest using Putty:

Start PuTTY, and:
- enter the IP address 
- enter vmguest name
- press *Save*
- press *Open*<br>
![starting_putty](https://github.com/DoriCastilla/Eramba-virtual-machine/assets/170856411/50df4e01-a969-43cf-8ee7-1f5732cd2052)

Login trough putty to the eramba vmguest, remember:
Login username: eramba
Login password: eramba 

### Editing Network Configuration:
In putty session: 
```
sudo nano /etc/netplan/50-cloud-init.yaml
```

Delete the rows in bright green and pink or disable it adding # at line start and write down:
```
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
     dhcp4: no
     addresses: [192.168.140.156/24]
     gateway4: 192.168.140.2
     nameservers:
       addresses: [8.8.8.8,8.8.4.4]
```
Where **ens33** can be different in your case.
Where IP  address might be different and here you must to change the 4rt octet for a random number above 1 and below 255.
Where gateway4 is always the 1st, 2on, and 3rt octets of your IP and the 4th. always a 2, at least you hak it.<br>
To exit: **Ctrl+X** <br>
Save modified buffer? **Y**
```
sudo netplan apply
```

Here you will lost connection in Putty with your eramba VMguest because its IP is changed. 
Close the Putty session and start it again updating the new IP you set.

### Building the Eramba Server:

In Putty you get into the session with the updated IP, so, you are again in your VMguest: 
```
cd /home/docker/ 
```
```
sudo docker compose -f docker-compose.simple-install.yml up -d 
```
And watch the magic!.

### Opening Eramba:

Create the URL with your IP plus the port, in my case: *http://192.168.140.156:8443*<br>
Open your Web browser and write down your eramba url.

### Fixing Local host issues:

Back to Putty, if you are not in the directory home/docker, go there again: 
```
cd /home/docker/ 
```
Turn off the eramba server:
```
sudo docker compose -f docker-compose.simple-install.yml down 
```
```
sudo docker compose -f docker-compose.simple-install.yml down 
```
Look for the row **PUBLIC_ADRESS=https://192.168.140.156:8443<br>
To exit: **Ctrl+X** <br>
Save modified buffer? **Y**

Then update your eramba server:
```
sudo docker compose -f docker-compose.simple-install.yml up
```

### Login in Eramba:

Back to the Web Broser where you get the acces to Eramba interface you can log in with: 
username: admin 
password: admin

Eramba is running and ready for playing, my recomendation is to make a snapshot in VMware Workstation, in case you break it. 


