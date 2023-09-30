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








