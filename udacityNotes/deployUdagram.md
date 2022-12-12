# Udagram Deployment

## Setup run on local machine

```bash
# clone repository
git clone https://github.com/udacity/nd0067-c4-deployment-process-project-starter.git dp

# change git remote to own github account
cd dp
git remote remove origin
git remote add origin https://github.com/w314/deploymentPractice.git

# add ./udagram/set_env.sh to .gitignore
echo -e "\n.set_env.sh" >> ./udagram/.gitignore 

# make initial git commit
git add .
git commit -m 'chore: Initial commit'
git push origin master

```

## Try run locally with `aws` `rds`

```bash
# install node modules
cd udagram/udagram-api
npm install --production

# add environmental variables
# (.env is alredy in .gitignore)
echo '
POSTGRES_HOST=database-1.cdzpkohhdjsy.us-east-2.rds.amazonaws.com
POSTGRES_DB=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=haladokVele
JWT_SECRET=mysecretstring' > .env

# build app
npm run build

# start backend server
npm start

```
