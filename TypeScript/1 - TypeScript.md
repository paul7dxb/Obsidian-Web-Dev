- Builds up on JS
- Can be used in combination with React

# Intro

- [Website link](https://www.typescriptlang.org/)

- A superset to JS
	- Extends JS
	- The base JS does not changes
	- Adds features
		- Static typing instead of the dynamic typing

# Installation

- Requires Node.js to be [[Frameworks - React.js/2 - Setup#Install Node.js|installed]]

```bash
npm init -y
npm install typescript --save-dev
```

- Invoke compiler
	- Does not run in the browser
	- Requires compilation to JS
		- Type annotations will be removed but notifies you of the errors

```bash
npx tsc
```

Or compile one file:
```bash
npx tsc .\with-typescript.ts
```

- Will create a new .js file