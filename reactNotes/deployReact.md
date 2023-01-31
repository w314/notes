react, deploy, github

# Deploy React App

## Deploy React App created with `Vite`
### 1. create app 
```shell
# create app
npm create vite

# cd into app direcotry
cd <app_name>

# install node packeges
npm install

# open in VSCode
code -n .
```
### 2. Set up GIT
```shell
# initiate git repository 
git init

# make initial commit
git add .
git commit -m 'feat: Initial commit'

# push content to remote repository
# add remote repo
git remote add origin <remote_repo_url>
git push -u origin master
```

### 3. Deploy App to github pages
- install [gh_pages](https://www.npmjs.com/package/gh-pages)
```bash
npm install --save gh-pages
```
- setup app for deployment
  - add `base: "/<repo_name>/",` to `vite.config.ts`
  - add `"homepage": "https://<user_name>.github.io/<repo_name>",` to `package.json`
  - add new scripts to `package.json` `scripts`
```bash
"predeploy": "npm run build",
"deploy": "gh-pages -d dist",
```
- deploy app
```bash
npm run deploy
```
(the `predeploy` script will run automatically)
