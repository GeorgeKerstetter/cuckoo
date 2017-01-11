# cuckoo-autoinstall
The script "cuckoo.sh" intends to perform a full base install of the modified Cuckoo sandbox on Ubuntu 16.04 following the steps listed here: https://infosecspeakeasy.org/t/howto-build-a-cuckoo-sandbox/27

This script is nearly complete, but still may have some bugs. I built it out of necessity after I re-installed Cuckoo a few times trying to get the setup correct. Each install used to take a few hours, whereas this script should complete in under 15 minutes on a reasonably powered machine.

One important thing to be aware of is that this script will generate a secure password for the database, but also will use that generated password for the "cuckoo" user account. The account should be reasonably secure, but be aware that the password will exist in a plaintext file. Please make sure to change that password if you want the account fully secured.

-Usage-
```
sudo ./cuckoo <cuckoo_path> <db_pass> <ip> <machinery>
```
**NOTE: Alternate install options have not been completed. For now, run without arguments.**

If no arguments are provided, it will default to the following and auto-generated values will be displayed at runtime:

Cuckoo Path: /opt

DB Password: Pseudo-random generated by hashing date and then base64 encoding

Public IP: Attempts to discover public IP and use it during install

Machinery: kvm

Steps that need to take place after running script:

-Build sandbox VMs in KVM

-Modify Cuckoo conf files for new sandbox VMs

-Create user/pass for web portal

```
sudo htpasswd -c /etc/nginx/htpasswd $USER
sudo chown root:www-data /etc/nginx/htpasswd
sudo chmod u=rw,g=r,o= /etc/nginx/htpasswd
sudo service nginx restart
```

Tested on Ubuntu Server 16.04.1 LTS
