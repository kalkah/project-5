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

A new index.html file was created and the configuration was inserted into the html file

**`sudo nano index.html`**

```
        <!DOCTYPE html>
        <html>
        <head>
            <title>My EC2 Instance</title>
        </head>
        <body>
            <h1>Welcome to my EC2 instance</h1>
            <p>Public IP: 18.208.198.58</p>
        </body>
        </html>

```

The ownership of the index.html was changed with this command: **`sudo chown www-data:www-data ./index.html`**

The default html file of Apache server was override with the command: **`sudo cp -f ./index.html /var/www/html/index.html`**

Apache was restarted to load the new configuration using **`sudo systemctl restart apache2`** command

<img width="436" alt="image" src="https://github.com/kalkah/project-5/assets/95209274/3270e0fd-5344-448b-a815-b6314dcc3fc7">

<img width="956" alt="image" src="https://github.com/kalkah/project-5/assets/95209274/6838950f-7363-4edd-8e2d-77345f3cbc4d">

## Configuring Nginx as Load Balancer

Nginx was installed in the ngnix EC2 server using the command below:

**`sudo apt update -y && sudo apt install nginx -y`**

Nginx installation was verified with the command below:

**`sudo systemctl status nginx`**

<img width="944" alt="image" src="https://github.com/kalkah/project-5/assets/95209274/cae09c33-eab0-4c17-a5dd-0ba56b510465">

Nginx configuration file was opened with the command below:

**`sudo nano /etc/nginx/conf.d/loadbalancer.conf`**

The follwoing configuration was added into the ngnix configuration file so that nginx will act as load balancer.

```
  
        upstream backend_servers {

            # your are to replace the public IP and Port to that of your webservers
            server 18.208.198.58:8000; # public IP and port for webserser 1
            server 34.235.171.222:8000; # public IP and port for webserver 2

        }

        server {
            listen 80;
            server_name 34.229.52.105; # provide your load balancers public IP address

            location / {
                proxy_pass http://backend_servers;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            }
        }
    

```

**upstream backend_servers** defines a group of backend servers. The **server** lines inside the **upstream** block list the addresses and ports of backend servers. 
**proxy_pass** inside the **location** block sets up the load balancing, passing the requests to the backend servers.  The **proxy_ser_header** lines pass necessary header to the backend servers to correctly handle the request.

The configuration was tested using **`sudo nginx -t`** command.

<img width="422" alt="image" src="https://github.com/kalkah/project-5/assets/95209274/2e471a09-9062-4049-b89f-03702115001f">

Nginx was restarted to load the new configuration using **`sudo systemctl restart nginx`** command

Using the public address of the nginx load balancer, the same webpage served by the webservers can be seen as shown below:

<img width="960" alt="image" src="https://github.com/kalkah/project-5/assets/95209274/39c15fc9-31fd-413a-b280-82eca11329a5">

