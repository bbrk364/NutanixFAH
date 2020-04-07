Instructions assembled via numerous sources by Peter Walker - @vPeteWalker
#
Thanks to these folks for their assistance:  
John Rehmert  
#
Use at your own risk. I am not responsible for any cost, damages, etc. incurred by using the following script.  
If you intend on using this outside of equipment you personally own, be sure to receive approval to utilize said equipment.  
The goal is to allow both Nutanix Acropolis Operating System (AOS) and Community Edition (CE) users to participate with this worthy endeavor, with as few barriers as possible. For example, Prism Central (PC) or CALM (Cloud Application Lifecycle Management) are not required.  
Please feel free to use or modify these instructions as you see fit. I put this together to simplify the adoption of Folding at Home.  
Thank you for taking the time to join the Folding At Home community.  Have a wonderful day.
#
The following instructions will help you install Ubuntu Linux 16.04 LTS, and anonymously join the Nutanix team.  I've included instructions on how you can modify the user and passkey, which can be obtained by creating an account on Foldingathome.org.
#
Main location for Ubuntu images. Recommend visiting this before you deploy, to ensure you have the latest version:  
https://cloud-images.ubuntu.com/releases/xenial/release/  
Specific download location for Ubuntu 16.04 LTS image. Upload this image to your cluster before proceeding.  
https://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.img.  
#
Default username and password  
U: ubuntu  
P: nutanix/4u  
#
Paste the following into the Guest Customization field when creating a new VM:  
```  
#cloud-config  
password: Fold@Ntnx  
chpasswd: { expire: False }  
ssh_pwauth: True  
hostname: NutanixFAH  
runcmd:  
  - setenforce 0  
  - sed -i s/^SELINUX=.*$/SELINUX=disabled/ /etc/selinux/config  
  - systemctl disable firewalld  
  - systemctl stop firewalld  
  - yum -y update  
  - yum -y install epel-release  
  - yum -y install wget  
 - wget https://download.foldingathome.org/releases/public/release/fahclient/centos-6.7-64bit/v7.5/fahclient-7.5.1-1.x86_64.rpm  
 - wget https://download.foldingathome.org/releases/public/release/fahcontrol/centos-6.7-64bit/v7.5/fahcontrol-7.5.1-1.noarch.rpm  
 - rpm -u --nodeps fah*.rpm  
 - /etc/init.d/FAHClient stop  
 - sleep 15  
 - wget -O /etc/fahclient/config.xml https://github.com/vPeteWalker74/NutanixFAH/raw/master/config.xml  
 - reboot  
```  
Connect to any CVM and run the following before powering on the VM:  
```
acli vm.serial_port_create <VM_NAME> index=0 type=kNull
```
Power on VM, launch the console and select VNC to connect.
