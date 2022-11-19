# NFS and AutoFS for In-Direct Map share:
AutoMounting User Home Directories:

    Note: users name with it's correspondinguidandgidmust be the same on both nfs server and nfs client computer.

## NFS service side:

Install NFS package:

`nfserver ~$ sudo dnf install nfs-utils -y`

Create a user called user30 with UUID 3000 and assign a password:
```
nfserver ~$ sudo useradd -u 3000 user30
nfserver ~$ sudo echo 12345678 | sudo passwd --stdin user30
```

Add nfs service to the firewall daemon:
```
nfserver ~$ sudo firewall-cmd --add-service nfs --permanent
nfserver ~$ sudo firewall-cmd --reload
```

Enable and start nfs service:
```
nfserver ~$ sudo systemctl enable --now nfs-server
nfserver ~$ sudo systemctl status nfs-server
```

Edit the exports file and add the directive:
```
nfserver ~$ sudo vi /etc/exports
/home   nfs-client(rw)
```

Export the share in the /etc/exports file:

`nfserver ~$ sudo exportfs -avr`

## NFS Client side:

Install AutoFs package.

`nfs-client ~$ sudo dnf install autofs -y`

Create a user called user30 with UUID 3000 and assign a password.
```
nfs-client ~$ sudo useradd -u 3000 user30
nfs-client ~$ sudo echo 12345678 | sudo passwd --stdin user30
```

Create an umbella mount point to automount the user's home directory:

`nfs-client ~$ sudo mkdir /nfshome`

Edit the /etc/auto.master file and add the /nfshome directory.
```
nfs-client ~$ sudo vi /etc/auto.master
/nfshome    /etc/auto.master/auto.home
```

Create the /etc/auto.master.d/auto.home file and add the directive.
```
nfs-client ~$ sudo vi /etc/auto.master.d/auto.home
*   -rw     nfserver:/home/&
```