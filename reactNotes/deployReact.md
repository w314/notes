react, deploy, github

# Deploy React App created with `Vite`
- [deploy to github pages from vite](https://towardsdev.com/deploying-react-application-to-github-pages-with-vite-2d3e32ae97e7)

- create app `npm create vite`
- cd into app directory
- `npm install`
- `code -n .` (open in VS code)
- initiate git repository: `git init`
- add remote repo: `git remote add <remote_repo_url>`
- add `base: "/",` to `vite.config.ts`
- add `"homepage": "https://<user_name>.github.io/<repo_name>",` to `package.json`
- run `npm install gh-pages --save-dev` to install [gh_pages](https://www.npmjs.com/package/gh-pages)
- add `"deploy": "npm run build && gh-pages -d dist"` to `package.json` `scripts`
- remove `dist` directory from `.gitignore`
- run `npm run deploy` to deploy
