# project-5

## Load Balancing and Ngnix

The aim of this project is to setup basic load balancer using nginx.

### Provisioning EC2 Instance

Three EC2 instances  were provisioned, 2 instances were configured as webserver and the third instances as nginix. The webservers will be running on port 8000 and apache webserver will be installed on the two EC2 instances.

<img width="737" alt="image" src="https://github.com/kalkah/project-5/assets/95209274/9e504cba-4d09-407e-9896-39e6163a669f">

Apache was installed on the two webserver using the command below:

**`sudo apt update -y &&  sudo apt install apache2 -y`**

**`sudo systemctl status apache2`** command was used to verify that Apache is running on the webservers

<img width="496" alt="image" src="https://github.com/kalkah/project-5/assets/95209274/581a2fd2-b8fb-4502-bcb0-5678bebee272">

<img width="495" alt="image" src="https://github.com/kalkah/project-5/assets/95209274/e2db6215-52d5-4f49-bfdd-80d3c36a1b74">

## Configuring Apache to serve a page showing its public IP

Apache was configured to serve content on port 8000 by editing `/etc/apache2/port.conf` file using nanao text editor

**`sudo nano /etc/apache2/ports.conf`**
A new Listen directive was added for port 8000

<img width="586" alt="image" src="https://github.com/kalkah/project-5/assets/95209274/ff267a86-8941-4feb-8631-8478422c6d23">

The virualhost port in the file `/etc/apache2/sites-available/000-default.conf` was change from 80 to 8000 using nano text editor

**`sudo vi /etc/apache2/sites-available/000-default.conf`**

<img width="680" alt="image" src="https://github.com/kalkah/project-5/assets/95209274/27e99387-0cae-4879-8342-dd7451365d7c">

Apache was restarted to load the new configuration using **`sudo systemctl restart apache2`** command







