# Ansible Quick Management #

### When you want to run a quick configuration change without bothering any ssh-key for authentication ###

- run the update2.yml using your own root login and password to the target server/s, using `$ ansible-playbook -K update2.yml`

- you can add and run any other yml file that suites your needs.

- This is is the quickest configuration changes to do without creating ssh-keys and defining them into the ansible.cfg file.