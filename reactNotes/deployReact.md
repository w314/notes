react, deploy, github

# Deploy React App

## Deploy React App created with 

### 1. Set up GIT
```shell
# add remote repo
git remote add origin <remote_repo_url>
git push -u origin master
```
  
### 2. If using `VITE`
In `vite.config.ts` add:
```typescript
base: '/<repo_name>/'
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
"deploy": "gh-pages -d <folder_name>",
```
Deploy app:
```bash
npm run deploy
```
- the `predeploy` script will run automatically
- it will create a gh-pages branch in the github repo and use it to deploy the app

### Problem Solving

#### Error: `fatal: A branch named 'gh-pages' already exists.`
- Complains about already existing gh-pages branch but there are no gh-pages branch on github or in the local repo.
- Happens when a deploy was unsuccesfull before and stopped in the middle of the process.

Run :
```
rm -rf node_modules/.cache/gh-pages
```