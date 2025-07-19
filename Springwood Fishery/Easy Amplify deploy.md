- Use git like we normally do
- Link Amplify to rebuild when it detects a commit to main

# Fork My repo

- https://github.com/paul7dxb/wildrydes-site
	- This is the S3 files they link to in the tutorial
	- You can make it public or private, doesn't matter

# Deploy with Amplify

1. Go to AWS amplify in web console
2. Click "new app"
	1. Host web app
		1. ![[Pasted image 20231018141618.png|200]]
	2. ![[Pasted image 20231018141640.png|500]]
	3. Authorize Amplify to access your GitHub ( I have already set this up so found these steps [here](https://docs.aws.amazon.com/amplify/latest/userguide/setting-up-GitHub-access.html))
		1. If this is the first time connecting a GitHub repository, A new page opens in your browser on GitHub.com, requesting permission to authorize AWS Amplify in your GitHub account. Choose **Authorize**.
		2. Next, you must install the Amplify GitHub App in your GitHub account. A page opens on Github.com requesting permission to install and authorize AWS Amplify in your GitHub account.
		3. Select the GitHub account where you want to install the Amplify GitHub App.
		4. To limit the installation to the specific repositories that you select, choose **Only select repositories**. Make sure to include the repo for the app that you are migrating in the repos that you select.
		5. Choose **Install & Authorize**.
3. You are redirected to the **Add repository branch** page for your app in the Amplify console.
	- If you added the wrong repo you can change by using the choose repos through View GitHub permissions
	- ![[Pasted image 20231018141816.png]]
	- ![[Pasted image 20231018142458.png]]
	- Save
	- Go back to amplify

4. In the **Recently updated repositories** list, select the name of the repository to connect.
	- ![[Pasted image 20231018142547.png]]

5. In the **Branch** list, select the name of the repository branch to connect.
	1. main
6. Choose **Next**.
7. On the **Configure build settings** page, choose **Next**.
	1. Tick "Allow AWS Amplify to automatically deploy all files hosted in your project root directory"
8. On the **Review** page, choose **Save and deploy**.

# View deployment

- After selecting deploy or navigating to your app now in amplify you will see the state of the deployment
	- Provision
	- Build
	- Deploy

![[Pasted image 20231018142825.png]]

- Once they are all green select the link under the left hand side window to take you to your site

![[Pasted image 20231018142907.png]]

- You should now see your site

![[Pasted image 20231018142931.png]]

# Deploying Changes

- When you make a commit to main the build and deploy process will start again
- For the first 12 months of you account you get 1,000 build minutes per month so you should be okay after that its $0.01 per minute