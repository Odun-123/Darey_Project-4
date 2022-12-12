# MEAN STACK DEPLOYMENT TO UBUNTU IN AWS

Step 1: Creating an AWS instance & Connecting to it using Windows Terminal

Created an Amazon account and provisioned an Ubuntu Server 22.04 LTS (HVM), SSD Volume Type EC2 Instance with a free tier option.

Step 2: Install NodeJs

I updated ubuntu with the command sudo update and upgrade with sudo apt upgrade

Then i now ran 

sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates

curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

Then I now ran the code below to install nodejs

' sudo apt install -y nodejs'
