ssh, linux, aws

# SSH

## Resources:
- [How to generate and manage ssh keys on Linux](https://linuxconfig.org/how-to-generate-and-manage-ssh-keys-on-linux)
- [SSH Keys theory](https://www.youtube.com/watch?v=dPAw4opzN9g)
- [How to log into AWS server with ssh](https://www.youtube.com/watch?v=8UqtMcX_kg0)


## About SSH

- `SSH` stands for secured shell

- The ssh key pair consists of two files, a public key and a private key.

- The public key can be generated from the private key  but not vice versa.

## The autorization process

1. The server send a random string encrypted by the public key to the client.
1. The client decrypts it with the private key, does a calculation on the decrypted string and send back the result of the calculation to the server.
1. The server can verify the client could decrypt the string, which is only possible with the private key and accepts the client's request for connection


## How to setup SSH authorizatio


### On the server

- SSH authorization must be allowed by in the `/etc/ssh/sshd.config` file by setting the`PubkeyAuthentication` option to `yes`
- 
```bash

```
- Linux: in your terminal use the `ssh` command to connect to servers


### Generate a key pair 
In the terminal run
```bash
ssh-keygen
```