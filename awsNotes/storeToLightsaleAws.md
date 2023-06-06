# Store to AWS Lightsale
- create instance on AWS
  - operation system only
  - select ssh key (store-key)
- attach permanent ip
- ssh to client `ssh ubuntu@<IP ADDRESS>
- run:  
```bash 
sudo apt-get update
```
```bash
sudo apt-get upgrade
```
- install node
```bash
sudo apt-get install nodejs npm
```
- clone repository
- cd into repository
- run `npm install`
- install docker with
```bash
sudo apt install docker.io
```
- install docker compose with
```bash
sudo apt install docker-compose
```
- create `.env` file with environment variables
`
- run
```bash
sudo docker-compose up -d
```


by-step guide to help you get started:

First, create an instance in AWS Lightsail. You can choose the operating system and the instance plan that best fits your needs.

Once the instance is up and running, connect to it using SSH. You can use the SSH client of your choice to connect to the instance.

Install Node.js and npm on the instance. You can do this by running the following command:

sudo apt-get install nodejs npm
Next, clone your Node.js Express backend repository to the instance. You can use Git to clone the repository:

git clone <repository-url>
Install the dependencies for your backend by running the following command in the root directory of your project:

npm install
Start your backend by running the following command:

npm start
This will start your backend on the default port (usually 3000).

Finally, configure your instance's firewall to allow traffic on the port your backend is running on. You can do this by adding a custom rule to the firewall:

sudo ufw allow <port-number>
Replace <port-number> with the port your backend is running on.


nc -4 -d -z -w 1 ${34.225.53.22} ${3001} &> /dev/null
if [[ $? == 0 ]]
then
    # Port is reached
    echo "Service is online!"
    exit 0
else
    # Port is unreachable
    echo "Service is offline!"
    exit 1
fi




[How to run nodejs app on nodejs lightsale](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-quick-start-guide-nodejs)
## connect
```bash
ssh ubuntu@34.225.53.22
```

## Setup
```bash
sudo apt-get update
```
```bash
sudo apt-get upgrade
```
- [install docker](https://www.simplilearn.com/tutorials/docker-tutorial/how-to-install-docker-on-ubuntu)



