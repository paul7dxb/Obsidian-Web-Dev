CD = Continuous Deployment

# Configure Amplify Build

- Include the backend

```bash
amplify console
? Which site do you want to open? AWS console
```

- On Web page
	- Left pane
	- App Settings
	- Build Settings
	- Add backend section

```YML
version: 1
backend:
  phases:
    build:
      commands:
        - '# Execute Amplify CLI with the helper script'
        - amplifyPush --simple
frontend:
  phases:
    preBuild:
      commands:
        - yarn install
    build:
      commands:
        - yarn run build
  artifacts:
    baseDirectory: build
    files:
      - '**/*'
  cache:
    paths:
      - node_modules/**/*
```

- Save
- Build Image Settings
	- Edit
	- Add Package Version Override
	- Amplify CLI

- On frontend deployment page on AWS
	- Update frontend branch to point to backend environment
	- Continuous deployment set up 'edit' <- click
	- [Add Amplify Service Role if required](https://docs.aws.amazon.com/amplify/latest/userguide/how-to-service-role-amplify-console.html)
	- Change environment to staging
	- Save

- Commit Git changes to main to start new build