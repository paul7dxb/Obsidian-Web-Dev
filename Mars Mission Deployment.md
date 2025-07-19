# Fork

- Fork
	- If you change the fork name change the base in `vite.config.ts` to match

# Run the build Action

- Settings
	- Pages
	- Build & deployment
		- Source: GitHub Actions
	- (I couldn't work out how to find the action here so went back to the repo then to `.github/workflows ` > `github-pages.yml` > view runs > "I understand" > Github Pages (on LHS bar) > run workflow > run workflow )
	- Let it finish running

# Site is live

- Site is now built and can go to it
	- Settings
	- Pages
	- "your site is live at..."

## ...but no API key

API key:
- Environments
- github-pages
- Environment secrets
	- Add a secret
		- `VITE_NASA_API_KEY`
		- Your API key value

- At this point my API key still wasn't coming in after running the action again 🤷

- Had to make this change in the action but hopefully someone can tell me what I did wrong:

github-pages.yml:
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    environment: github-pages  # Added this line

```

- After committing this change to main it should trigger the build action again
	- Can view by going to actions

- Should now be able to use the site with API key 🥳🥳

# Custom URL 👀

- If anyone is keen to get their own site to link in ( e.g mars-mission.your-name.com ) happy to help set it up with you in some free time