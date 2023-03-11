# Deployment Steps

![[Image_React_Server_Deployment.png]]

# Building Code For Production

- Highly optimised and tranformed code

```bash
npm run build
```

- This outputs the build folder
	- This is what is deployed
	- Has chunks from lazy loading
	- Includes thrid party packaged code including React

# Deploying

- React SPA is a static page so can be hosted as such
	- [[Static Hosting|Firebase Static Hosting]]