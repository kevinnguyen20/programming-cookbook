# Programming Cookbook

## FTP

Source: https://linuxconfig.org/how-to-setup-and-use-ftp-server-in-ubuntu-linux

### vsftp installation

```
sudo apt install vsftpd
```

### Configure vsftpd server

It’s always best practice to keep a backup copy of the original config file, just in case something goes wrong later. Let’s rename the default config file:

```
sudo mv /etc/vsftpd.conf /etc/vsftpd.conf_orig
```

```
sudo nvim /etc/vsftpd.conf
```

```
listen=NO
listen_ipv6=YES
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
dirmessage_enable=YES
use_localtime=YES
xferlog_enable=YES
connect_from_port_20=YES
chroot_local_user=YES
secure_chroot_dir=/var/run/vsftpd/empty
pam_service_name=vsftpd
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
ssl_enable=NO
pasv_enable=Yes
pasv_min_port=10000
pasv_max_port=10100
allow_writeable_chroot=YES
```

Ubuntu’s built-in firewall will block FTP traffic by default, but the following command will create an exception in UFW to allow the traffic: 

```
sudo ufw allow from any to any port 20,21,10000:10100 proto tcp
```

With the configuration file saved and the firewall rules updated, restart vsftpd to apply the new changes: 

```
sudo systemctl restart vsftpd
```
