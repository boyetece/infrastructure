# fail2ban post installation step: #

After installing fail2ban using the sshd_default.config. You must also edit the /etc/ssh/sshd_config file to indicate that the `MaxAuthTries 3` and `PermitEmptyPasswords no` to match the fail2ban sshd_default.conf file where `maxretry = 3`. Not doing so may result in fail2ban to not consistently block brute force attack.