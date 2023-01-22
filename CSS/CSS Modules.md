- Requires compiling so needs to be supported by project
	- React can use it


## Usage

- Rename css file to `filename.module.css`
- Impor CSS file in component file slightly differently

```JS
import styles from './filename.module.css'
```

- Apply classes by object access

```JSX
className={styles.class}
className={styles['class']}
//Examples
className={styles.button}
className={styles['class-with-hyphens']}
```

- Will create a unique identifier at compilation to avoid CSS clashes

![[Pasted image 20230122083415.png]]
