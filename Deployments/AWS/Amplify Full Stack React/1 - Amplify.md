- Used to host Web deployments such as React
- Can be linked to build from github

[Tutorial on Full Stack React deployment with Amplify](https://aws.amazon.com/getting-started/hands-on/build-react-app-amplify-graphql/)

# Build React App

- Create React app [[Frameworks - React.js/2 - Setup|the usual way]] and create repo for it on github to build on AWS Amplify from

# Set up AWS Amplify

- Go to AWS Amplify and build from github repo using default settings (auto detects build)
- Update to repo will automatically trigger build process

# Set Up Backend

- If neccessary install and configure [[2 - Amplify CLI]]
- On Amplify web page go to ' banckend environments' and set up 'Amplify Studio'
- On Backend Environments page click on 'local setup instructions' and copy the command that will be similar to

```bash
amplify pull --appId <someCharacters> --envName staging
```

```bash
? Choose your default editor: Visual Studio Code
? Choose the type of app that you're building javascript
? What javascript framework are you using react
? Source Directory Path:  src 
? Distribution Directory Path: build
? Build Command:  npm run-script build
? Start Command: npm run-script start
? Do you plan on modifying this backend? Y
```

# View amplify Console

```bash
amplify console
? Which site do you want to open? AWS console
```