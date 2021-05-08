# learn from [https://github.com/gitname/react-gh-pages.git](https://github.com/gitname/react-gh-pages.git)

# Deploying a React App\* to GitHub Pages

\* created using `create-react-app`

# Introduction

This repository contains the files related to the app. The `master` branch contains the app's source code (the code the app's developers edit), and the `gh-pages` branch contains a _built_ version of the app (i.e. the code that GitHub Pages serves to the app's visitors).

The remainder of this document contains a tutorial on creating a React app (using `create-react-app`) and deploying that app to GitHub Pages.

# Tutorial

## Prerequisites

1. An adequate version of [`Node.js`](https://nodejs.org/) is installed. Here's the adequate version I use:

   ```sh
   $ node --version
   v6.10.1
   ```

2. An adequate version of [`npm`](https://nodejs.org/) is installed. Here's the adequate version I use:

   ```sh
   $ npm --version
   3.10.10
   ```

3. An adequate version of [`create-react-app`](https://github.com/facebookincubator/create-react-app) is installed. Here's the adequate version I use:

   ```sh
   $ create-react-app --version
   1.3.1
   ```

   In the case of `create-react-app`, you can either install it globally (i.e. `$ npm install -g create-react-app`) or install it locally (i.e. `$ npm install create-react-app`). If you choose the latter, you will have to specify its path whenever you invoke it (e.g. `path/to/node_modules/.bin/create-react-app`).

4. A [GitHub](https://www.github.com) account. :octocat:

5. A command-line Git client [setup according to GitHub](https://help.github.com/articles/set-up-git/).

## Procedure

1. **Create an _empty_ repository on GitHub.** (2 minutes)

   - For this tutorial, I'll create a repository named `intro` from github

2. **Create a new React app on your computer.** (5 minutes)

   ```sh
   $ npx create-react-app intro
   ```

3. **Install the `gh-pages` package as a "dev-dependency" of the app.** (1 minute)

   ```
   $ cd intro
   $ npm install gh-pages --save-dev
   ```

   - The commands shown in the following steps can all be issued from within the app's folder.

4. **Add some properties to the app's `package.json` file.** (3 minutes)

   - At the top level, add a `homepage` property. Define its value to be the string `http://{username}.github.io/{repo-name}`, where `{username}` is your GitHub username, and `{repo-name}` is the name of the GitHub repository you created in step 1. Since my GitHub username is `gitname` and the name of my GitHub repository is `intro`, I added the following property:

   ```js
   //...
   "homepage": "http://gitname.github.io/intro"
   ```

   - In the existing `scripts` property, add a `predeploy` property and a `deploy` property, each having the values shown below:

   ```js
   "scripts": {
     //...
     "predeploy": "npm run build",
     "deploy": "gh-pages -d build"
   }
   ```

5. **Create a git repository in the app's folder.** (1 minute)

   ```
   $ git init
   Initialized empty Git repository in C:/path/to/react-gh-pages/.git/
   ```

6. **Add the GitHub repository as a "remote" in your local git repository.** (1 minute)

   ```
   $ git remote add origin https://github.com/gitname/intro.git
   ```

   - This will make it so the `gh-pages` package knows where you want it to deploy your app in step 7.
   - At this time, there is only one branch in your git repo.
   - It will also make it so git knows where you want it to push your source code (i.e. the commits on your `master` branch) in step 8.

7. **Generate a _production build_ of your app, and deploy it to GitHub Pages.** (2 minutes)

   ```
   $ npm run deploy
   ```

   - That's it! Your app is now accessible at the URL you specified in step 4.
   - In my case, my app is now accessible at: https://gitname.github.io/intro/
   - I recommend exploring the GitHub repository at this point. When I explored it, I noticed that, although a `master` branch did not exist, a `gh-pages` branch did exist. I noticed the latter contained the _built_ app code, as opposed to the app's source code.

8. **Optionally, commit your source code to the "master" branch and push your commit to GitHub.** (1 minute)

   ```
   $ git add .
   $ git commit -m "Create a React app and publish it to GitHub Pages"
   $ git push origin master
   ```

   - I recommend exploring the GitHub repository once again at this point. When I did that, I noticed that a `master` branch now existed, and it contained the app's source code.
   - So, the `master` branch held the source code, and the `gh-pages` branch held the _built_ app code.

# References

1. [Facebook's tutorial on deploying a React app to GitHub Pages](https://facebook.github.io/create-react-app/docs/deployment#github-pages-https-pagesgithubcom)
