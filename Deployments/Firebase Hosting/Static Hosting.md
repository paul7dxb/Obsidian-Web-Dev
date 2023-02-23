- [Official Docs](https://firebase.google.com/docs/hosting)

# How to Use

- Build the React application first. See [[31 - Deployments#Building Code For Production|Building React App]]
- login
- Create New Project

![[Image_Firebase_Static_Deploy_Project_Name.png]]

- Build
- Hosting
- Get Started

- Install Firebase Hosting

```bash
npm install -g firebase-tools

firebase login

firebase init
```


![[Image_Firebase_Static_Deploy_Selection.png]]

- Use an existing project
- Select Project created above
	- react-deployment-demo
- Slect folder to use
![[Image_Firebase_Static_Deploy_Questions.png]]

- Creates two new files that are connected to firebase

# Deploy

- Uploads files from build folder to firebase

```
firebase deploy
```

- This will return a URL to visit

![[Image_Firebase_Static_Deploy_Final_Output.png]]

# Turn Off Site

```bash
firebase hosting:disable
```

# Choosing SPA

- Navigation is provided by react-router-dom package
	- Executes in the browser

# Deploying changes

```bash
npm run build
firebase deploy
```