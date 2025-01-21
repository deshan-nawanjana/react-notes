# React Prerequisites

- [Git - Version Control System](#git-version-control-system)
- [NVM - Node Version Manager](#nvm-node-version-manager)
- [NPM - Node Package Manager](#npm-node-package-manager)
- [Vite - Frontend Build Tool](#vite-frontend-build-tool)

## Git: Version Control System

📦 Installation (Windows / Unix) [https://git-scm.com/downloads](https://git-scm.com/downloads)

📕 Docs [https://git-scm.com/docs](https://git-scm.com/docs)

💻 Useful Commands

`git init` - *Initiate a Git repository*

```bash
mkdir my-repo
cd my-repo
git init
```

`git clone` - *Download repository from a remote location*

```bash
git clone https://github.com/mrdoob/three.js
```

`git status` - *Check modified / untracked files status*

```bash
git status
```

`git add` - *Stage file to commit*

```bash
# stage all files
git add .
# stage single file
git add sample.txt
# stage all jsx files
git add *.jsx
```

`git reset` - *Unstage currently staged files*

```bash
git reset
```

`git commit` - *Commit currently staged files with a message*

```bash
git commit -m "My Commit Message"
```

`git pull` - *Download all the changes in the remote repository*

```bash
git pull
```

`git push` - *Upload all the local committed changes to the remote repository*

```bash
git push
```

## NVM: Node Version Manager

📦 Installation
- Windows [https://github.com/coreybutler/nvm-windows](https://github.com/coreybutler/nvm-windows)
- Unix [https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm)

📕 Docs [https://github.com/nvm-sh/nvm#readme](https://github.com/nvm-sh/nvm#readme)

💻 Useful Commands

`nvm list` - *List all the Node version currently installed*

```bash
nvm list
```

`nvm install` - *Download and install any Node version*

```bash
# install the latest stable version
nvm install node
# install a specific version
nvm install 20.15.0
```

`nvm use` - *Switch to relevant Node version*

```bash
# switch to the installed latest version starting with 20 
nvm use 20
# switch to a specific version
nvm use 18.18.2
```

`nvm uninstall` - *Uninstall a Node version*

```bash
# uninstall the specified version
nvm uninstall 13.14.0
```

## NPM: Node Package Manager

📦 Node Installation
  - NVM - `nvm install latest` / `nvm install v20.15.0`
  - Manual - [https://nodejs.org/en/download](https://nodejs.org/en/download)

📕 Docs [https://docs.npmjs.com/](https://docs.npmjs.com/)

💻 Useful Commands

`npm create` - *Create a new project*

```bash
# create a vite app
npm create vite@latest
```

`npm install` - *Install Node modules*

```bash
# install all the modules specified in package.json
npm install
# install the modules called axios to the project
npm install axios
```

`npm remove` - *Uninstall a Node module*

```bash
# uninstall the modules called axios from the project
npm uninstall axios
```

`npm run` - *Execute a script specified in package.json*

```bash
# start development server
npm run dev
# create a distribution build of project
npm run build
```

## Vite: Frontend Build Tool

📕 Docs [https://vite.dev/guide/](https://vite.dev/guide/)

📦 Create Vite Project

1. Execute following command

```bash
# create a vite app
npm create vite@latest
```

2. Type your project name

3. Use arrows in keyboard to select options:

```
React > Javascript
```

4. Execute following commands

```bash
# navigate into your project directory
cd my-app
# install node modules
npm install
# start development server
npm run dev
```

🗃️ File and Folder Hierarchy
- node_modules - *Modules installed from NPM*
- public - *Files to be served directly*
- src - *Project source files*
  - App.js - *Initial app component*
  - App.css - *Initial app styles*
  - index.css - *Default styles*
  - main.js - *React root render script*
- .gitignore - *Files to ignore by Git*
- eslint.config.js - *ESLint Configuration*
- index.html - *Root HTML template*
- package-lock.json - *Nested dependency structure*
- package.json - *Project details, commands and dependencies*
- README.md - *Markdown for documentation*
- vite.config.js - *VITE Configuration*
