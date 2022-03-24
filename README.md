# Programming Cookbook

## Fun

### Steam Locomotive

Source: https://www.linuxshelltips.com/sl-run-locomotive-train-in-terminal/

```
sudo apt install sl
```

Run the command to verify the installation. If installed and working correctly, you should see the train animation shown below.

```
sl
```

#### Basic Usage of SL (Steam Locomotive) in Linux

If you call the command with a parameter `-a`, it will show the train animation, with people on the train shouting for help.

```
sl -a
```

Parameter `-l` shows a smaller train in the animation.

```
sl -l
```

Similarly, with '-F' parameter, the train will appear as if it is flying, instead of going in a straight line.

```
sl -F
```

There is another parameter '-e' which will allow the user to close the animation with a Ctrl + C signal when used.

```
sl -e
```

## FTP

Source: https://linuxconfig.org/how-to-setup-and-use-ftp-server-in-ubuntu-linux

### How to setup and use FTP Server in Ubuntu Linux

#### vsftp installation

```
sudo apt install vsftpd
```

#### Configure vsftpd server

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

#### Create an FTP user

```
sudo useradd -m ftpuser
sudo passwd ftpuser
```

In order to verify that everything’s working properly, you should store at least one file in ftpuser’s home directory. This file should be visible when we login to FTP in the next steps.

```
sudo bash -c "echo FTP TESTING > /home/ftpuser/FTP-TEST"
```

#### Connect to FTP server via command line

```
sudo apt install ftp
```

```
ftp 127.0.0.1
```

As you can see in the screenshot above, we were able to login to the FTP server by specifying the username and password that we configured earlier. Next, let’s try issuing an ls command, which should list the test file that we created in previous steps.

```
ftp> ls
```

#### Allow anonymous access in vsftpd

So far, we’ve seen how to create new users that can access the FTP server. If you’d like others to be able to access your FTP server without giving a username and password, you can configure anonymous authentication. Follow the steps below to get it set up.

```
sudo nvim /etc/vsftpd.conf
```

Next, look for the anonymous_enable=NO line, and change the setting to YES.

```
anonymous_enable=YES
```

```
sudo systemctl restart vsftpd
```

To test out anonymous login, issue the ftp 127.0.0.1 command, use anonymous as your username, and a blank password. You should receive a 230 Login successful message as shown in the screenshot below.

#### Change default FTP port number

By default, the FTP protocol listens on port 21 for user authentication and port 20 for data transfer. However, we can change this behavior by making a small edit to the /etc/vsftpd.conf file. At the bottom of the file, use the listen_port directive to specify a different port for vsftpd to use. For example, adding the following line will instruct vsftpd to listen on port 2121:

```
listen_port=2121
```

