linux, connect, remote

## How to connect remotely to system
[How to Fix “Connection Refused By Port 22” on Ubuntu 22.04 LTS](https://itsubuntu.com/how-to-fix-connection-refused-by-port-22-on-ubuntu-22-04-lts/)

Port 22 is used by SSH on Ubuntu for communicating with other machines in the network to transfer data. Port 22 is also used to access the remote system.

The most common reason behind this error is  OpenSSH has not being installed on Ubuntu where you are trying to connect.  To see whether OpenSSH is installed or not, run the following command on a remote machine.
```bash
sudo apt list --installed | grep openssh-server
```
If you see nothing printed out on the console, then you do not have it installed. You can easily install OpenSSH using the following command:
```bash
sudo apt install openssh-server -y
```
```bash
sudo systemctl status ssh
```
Now, you can make it active with the following command
```bash
sudo systemctl start ssh
```
