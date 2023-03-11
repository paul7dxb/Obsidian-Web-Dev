- For more info on TypeScript start at the [[1 - TypeScript|Typescript section here]]

# Create React Project to use TypeScript

- Still use create react app
	- [Create React App with TS Docs](https://create-react-app.dev/docs/adding-typescript)

- Start new project with TS integration:
```bash
npx create-react-app my-app --template typescript
```

- Or add to existing project:
```bash
npm install --save typescript @types/node @types/react @types/react-dom @types/jest
```

# Start

- Same as before
- `npm start`
- TS is compiled to JS which is then further optimised
	- Compiling happens automatically and on build by react

# Files

- Files that inlcude JSX should be of type .tsx

# Dependencies

- Extra dependecies
	- Typescript
	- @types/
		- translation bridges between JS libraries at TS
		- Some libraries already have built in translation but ones that dont require these bridges

