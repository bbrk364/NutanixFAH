Created by Peter Walker - @vPeteWalker  
#
Use at your own risk. I am not responsible for any cost, damages, etc. incurred by using the following script.  
#
If you intend on using this outside of equipment you personally own, be sure to receive approval to utilize said equipment.  
#
The goal is to allow both Nutanix Acropolis Operating System (AOS) and Community Edition (CE) users to participate with this worthy endeavor, with as few barriers as possible. For example, Prism Central (PC) or CALM (Cloud Application Lifecycle Management) are not required.  
#
The following instructions will help you install Ubuntu Linux 16.04 LTS, and anonymously join the Nutanix team.  I've included instructions on how you can modify the user and passkey, which can be obtained by creating an acocunt on Foldingathome.org.  
#
Main location for Ubuntu images. Recommend visiting this before you deploy, to ensure you have the latest version: https://cloud-images.ubuntu.com/releases/xenial/release/  
Specific download location for Ubuntu 16.04 LTS image: https://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.img. Upload this image to your cluster before proceeding.  
#
Default username and password  
U: ubuntu  
P: nutanix/4u  
#
Required config to run on AHV.  
#cloud-config  
password: nutanix/4u  
chpasswd: { expire: False }  
ssh_pwauth: True  
wget https://download.foldingathome.org/releases/public/release/fahclient/debian-stable-64bit/v7.5/fahclient_7.5.1-64bit-release.tar.bz2  
tar -jxvf fahclient_7.5.1-64bit-release.tar.bz2  
wget https://ENTER CONFIG XML HERE  
./FAHClient --cpu-usage=100 --cpus=0 --user vPeteWalker --team 240445 --passkey=82cdc64762a44c2882cdc64762a44c28 --priority high --web-enable=true  
#
Connect to any CVM and run the following before powering on the VM:  
acli vm.serial_port_create <VM_NAME> index=0 type=kNull  
Power on VM, launch the console and select VNC to connect.  
