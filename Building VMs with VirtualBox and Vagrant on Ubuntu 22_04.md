<head><h1><strong>Building VMs with VirtualBox and Vagrant on Ubuntu 22_04 </strong></h1></head>
<body>
<button type="button"><p>Update and upgrade the package index in terminal:</p></button>
<p>~$ <style="color:blue">sudo apt update</p>
<p>Import VB package repositories keys:</p>
<p>~$</p><p style="color:blue">Sudo apt install curl -y</p>
<p>~$</p><p style="color:blue">curl https://www.virtualbox.org/download/oracle_vbox_2016.asc | gpg --dearmor > oracle_vbox_2016.gpg</p>
<p>~$</p><p style="color:blue">curl https://www.virtualbox.org/download/oracle_vbox.asc | gpg --dearmor > oracle_vbox.gpg</p>
<p>~$</p><p style="color:blue">sudo install -o root -g root -m 644 oracle_vbox_2016.gpg /etc/apt/trusted.gpg.d/</p>
<p>~$</p><p style="color:blue">sudo install -o root -g root -m 644 oracle_vbox.gpg /etc/apt/trusted.gpg.d/</p>
<p>Add the VirtualBox  repository:</p>
<p>~$</p><p style="color:blue">echo "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian $(lsb_release -sc) contrib" | sudo tee /etc/apt/sources.list.d/virtualbox.list</p>
<p>Install VirtualBox:</p>
<p>~$</p><p style="color:blue">sudo apt update</p>
<p>~$</p><p style="color:blue">sudo apt install -y linux-headers-$(uname -r) dkms
<p>~$</p><p style="color:blue">
<p>~$</p><p style="color:blue">
