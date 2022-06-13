# Project Requirements #

### In this project there are some prerequisites to be done before running the configuration yml files. ###

- create the sudoer_devop user in the directory - `/etc/sudoers.d/devop`
- create an ansible ssh keys that has no password using the `ed25519` encryption, to be use by devop user within the bootstrap.yml file.
- run the bootstrap.yml using your own root login and password to create the devop user on all the servers, using `$ ansible-playbook --ask-become-pass bootstrap.yml`
- when the devop user is created using the bootstrap.yml file, you can now run the site.yml using the devop user credentials. `$ ansible-playbook site.yml`