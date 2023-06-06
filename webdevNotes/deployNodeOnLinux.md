nodejs, ubuntu, express, deploy

## Resources

- [How to Deploy Node.js/Express.js Application on Ubuntu Server
  ](https://meetawaiszafar.medium.com/how-to-deploye-nodejs-expressjs-application-for-production-on-ubuntu-20-04-524e5c0b2dd8)
- [How To Set Up a Node.js Application for Production on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-20-04)

## Install Node.js

[How To Install Node.js on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04)

## Run App as Service in teh background

PM2 is a process manager for Node.js applications. It provides an easy way to manage and demonize applications (run them in the background as a service).

## Install Nginx

[How To Install Nginx on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04)

## Configue firewall

Finally, configure your instance's firewall to allow traffic on the port your backend is running on. You can do this by adding a custom rule to the firewall:

sudo ufw allow <port-number>
Replace <port-number> with the port your backend is running on.
