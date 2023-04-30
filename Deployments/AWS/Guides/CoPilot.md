- [tutorial link](https://aws.amazon.com/getting-started/guides/deploy-webapp-copilot/module-one/)

- Cloud9
	- CLI that can run docker
- Create new environment

- Install copilot on cloud9

```bash
curl -Lo copilot https://github.com/aws/copilot-cli/releases/latest/download/copilot-linux && chmod +x copilot && sudo mv copilot /usr/local/bin/copilot && copilot --help
```

- Clone web application

```bash
git clone https://github.com/aws-samples/aws-copilot-sample-service example 
cd example
```

- Initialise copilot

```bash
copilot init
```

- Answer questions
	- name application
	- Load balanced web server
	- Name service
	- Choose docker file

## Create an environment to run your application

```bash
copilot env init --name prod --profile default --app copilot-guide
```

## Deploy prod Environment

- May need to make temporary super user [[Cloud9#Make temporary super user for Cloud9|notes]]
```bash
copilot env deploy —name prod
copilot deploy
```

# Clean Up

- Delete the infrastructure with one command
	- If created temporary super user rememeber to delete them
	- If created Cloud9 environment delete it

```bash
copilot app delete
```