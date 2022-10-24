This lab shows how to provision your VM using a virtual box. Also, we will install the following packages:
1. Install (Virtual Box) [https://www.virtualbox.org/wiki/Downloads] 
2. Download your iso image ()
3. Install the following packages:
- vim 
sudo apt install vim -y
vim --version
- Curl
sudo apt curl vim -y
curl -v
- Telnet
sudo apt install telnet -y
telnet --version

- Unzip
unzip -v
sudo apt install unzip -y
- Wget
wget --version
sudo apt install wget-y
- Net-tools
net-tools --version
sudo apt install net-tools-y
- Htop
htop -v
sudo apt install htop -y
- Nmap
sudo apt install nmap -y
nmap -v
4. How to define your machine name:
type hosname
sudo vim /etc/hostname
delete the actual host name 
type DX2-486 for the new hostname
sudo reboot
hostname

5. Create a new user
getent passwd | grep victor
sudo useradd victor -m victor
getent passwd | grep victor
6. Install Nginx
sudo apt install nginx


curl localhost
mkdir /var/www/tutorial

sudo vim /var/www/tutorial/index.html

<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <title>Hello, Nginx!</title>
</head>
<body>
    <h1>Hello, Nginx!</h1>
    <p>We have just configured our Nginx web server on Ubuntu Server!</p>
</body>
</html>

sudo vim /etc/nginx/sites-enabled/default 

server {
       listen 81;
       listen [::]:81;

       server_name example.ubuntu.com;

       root /var/www/tutorial;
       index index.html;

       location / {
               try_files $uri $uri/ =404;
       }
}

sudo service nginx restart
curl localhost:81 