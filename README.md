This lab shows how to provision your VM using a virtual box.

### STEP 1. Install [Virtual Box](https://www.virtualbox.org/wiki/Downloads)
<br>

### STEP 2. Install [Vagrant](https://developer.hashicorp.com/vagrant/docs/installation) on your system, create a new folder and then create your VM based in a Debian image
<br>

```console
foo@bar:~$ mkdir my_project
foo@bar:~$ cd my_project
foo@bar:~$ vagrant init debian/buster64 
foo@bar:~$ vagrant up
foo@bar:~$ vagrant ssh
```
<br>

### STEP 3. Install the following packages:

- vim 
```console
vagrant@buster:~$ sudo apt install vim -y
vagrant@buster:~$ vim -v
```

- Curl
```console
vagrant@buster:~$ sudo apt install curl -y
vagrant@buster:~$ curl -v
```

- Telnet
```console
vagrant@buster:~$ sudo apt install telnet -y
vagrant@buster:~$ telnet -v
```

- Unzip
```console
vagrant@buster:~$ sudo apt install unzip -y
vagrant@buster:~$ unzip -v
```

- Wget
```console
vagrant@buster:~$ sudo apt install wget -y
vagrant@buster:~$ wget -v
```

- Net-tools
```console
vagrant@buster:~$ sudo apt install net-tools -y
vagrant@buster:~$ net-tools -v
```

- Htop
```console
vagrant@buster:~$ sudo apt install htop -y
vagrant@buster:~$ htop -v
```

- Nmap
```console
vagrant@buster:~$ sudo apt isntall nmap -y
vagrant@buster:~$ nmap -v
```

STEP 4. Define your machine name:

```console
vagrant@buster:~$ hostname
vagrant@buster:~$ sudo vim /etc/hostname
```
- delete the actual host name 
- type DX2-486 for the new hostname
- also add  "127.0.0.1 DX@-486" the new hostname to the hosts file

```console
vagrant@buster:~$ sudo vi /etc/hosts
```
- Restart the VM
```console
foo@bar:~$ vagrant ssh
vagrant@DX2-486:~$ hostname
```

### STEP 5. Create a new user
```console
vagrant@DX2-486:~$ getent passwd | grep victor
vagrant@DX2-486:~$ sudo useradd -m victor
vagrant@DX2-486:~$ getent passwd | grep victor
```

### STEP 6. Install Nginx
```console
vagrant@DX2-486:~$ sudo apt install nginx
vagrant@DX2-486:~$ curl localhost
vagrant@DX2-486:~$ sudo mkdir /var/www/tutorial
vagrant@DX2-486:~$ sudo vim /var/www/tutorial/index.html
```
- Use this html template
```html
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
```
- Edit the default website configuration
```console
vagrant@DX2-486:~$ sudo vim /etc/nginx/sites-enabled/default 
```
```json
server {
       listen 81;
       listen [::]:81;

       server_name example.debian.com;

       root /var/www/tutorial;
       index index.html;

       location / {
               try_files $uri $uri/ =404;
       }
}
```
- Restart the nginx service
```console
vagrant@DX2-486:~$ sudo service nginx restart
```
- Access the website
```console
vagrant@DX2-486:~$ curl localhost:81 
```
- Now you can destroy everything
```console
vagrant@DX2-486:`$ exit
foo@bar:`$ vagrant destroy
```