# Preparing for Kavita Infrastructure #

Infrastructure for this project must need to set up due to Cloudflare's non-support for non-standard port assigned to Kavita Server port 5000. In this setup, we need Nginx to do a reverse proxy for Kavita on port 5000, exposing Nginx port 80 for Kavita. With this, we can point our DNS Cloudflare record to the Linode instance with standard port 80.

Kavita Server will be installed as a Docker Container and Nginx would run on the localhost itself.  With will install the Nginx first then we will continue installing Kavita Server in our part 2 documentation.

```
~$ sudo apt update
~$ sudo install nginx -y
```