# Preparing for Kavita Infrastructure #

Infrastructure for this project must need to set up due to Cloudflare's non-support for non-standard port assigned to Kavita Server port 5000. In this setup, we need nginx to do a reverse proxy for Kavita on port 5000, exposing nginx port 80 for Kavita. With this, we can point our DNS Cloudflare record to the VPS instance with standard port 80.

Kavita Server will be installed as a Docker Container and nginx would run on the localhost itself.  With will install the nginx first then we will continue installing Kavita Server in our part 2 documentation.

```
~$ sudo apt update
~$ sudo install nginx -y
```
After this install, try browsing it using wwww.YOURWEBSITE.com. It should display the default Nginx webpage.
Go to the nginx configuration file and edit it.

```
~$ cd /etc/nginx/config.d
~$ sudo vim web.conf
```
Config File:

```
server {
    listen 80 default_server;
    server_name www.YOURWEBSITE.com YOURWEBSITE.com;

    location / {
        root    /var/www/html;
        # alias /var/www/html;
        # alias /usr/share/nginx/html;
        index   index.html;
    }

}

server {
root /var/www/html;
        listen 80;
        listen [::]:80;
        server_name SUBDOMAIN.YOURWEBSITE.com www.SUBDOMAIN.YOURWEBSITE.com;
        location / {
            proxy_pass         http://127.0.0.1:5000;
            proxy_redirect     off;
            proxy_set_header   Host $host;
            proxy_set_header   X-Real-IP $remote_addr;
            proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header   X-Forwarded-Host $server_name;
            proxy_set_header   X-Forwarded-Proto $scheme;
        }
}
```

Then reload nginx:

```
~$ sudo nginx -t
~$ sudo systemctl restart nginx
~$ sudo systemctl status nginx
```