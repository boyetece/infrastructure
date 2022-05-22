# NGINX configuration file #
This configuration file is in /etc/nginx/conf.d/

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