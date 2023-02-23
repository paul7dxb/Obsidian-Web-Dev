# Shortcuts

| Command | Description |
| --- | --- |
| Ctrl + Shift + arrow | duplicate in direction
| Ctrl + ' | Open terminal |
| Ctrl + Shift + f | Prettier reformat |
| Ctrl + / | Comment toggle selection |
| Alt + click | Multiple Cursors |
| multi-cursor | [[#Multi Cursor]] |
| alt + arrow | Move line up / down |
| Ctrl + Shift + K | Delete current line |
| Ctrl + \` | Toggle Terminal |
| Ctrl + L | Select Current Line |
| F2 | Rename a component and replace |

# Links:
https://cult.honeypot.io/reads/20-vs-code-shortcuts-developers/

# Multi Cursor

- Ctrl+D (Cmd+D on Mac) selects next occurrence of word under cursor or of the current selection
- Ctrl+K Ctrl+D moves last added cursor to next occurrence of word under cursor or of the current selection
- The commands use matchCase by default. If the find widget is open, then the find widget settings (matchCase / matchWholeWord) will be used for determining the next occurrence
- Ctrl+U (Cmd+U on Mac) undoes the last cursor action, so if you added a cursor too many or made a mistake, you can press Ctrl+U (Cmd+U on Mac) to go back to the previous cursor state. Adding cursor up or down (Ctrl+Alt+Up / Ctrl+Alt+Down) (Cmd+Alt+Up / Cmd+Alt+Down on Mac) now reveals the last added cursor to make it easier to work with multiple cursors on more than 1 viewport height at a time (i.e. select 300 lines and only 80 fit in the viewport). 


# Emmet in JS file

-   Open Command Palette (Ctrl + Shift + P)
-   Open Settings (JSON)
-   Add to the end:
	- "emmet.includeLanguages": { "javascript": "html" }

# Addons

## Prettier
- Format document

## Arrow Function Snippets


```JS
// afeea
  (arg) => {
    █
  }
```

https://marketplace.visualstudio.com/items?itemName=deinsoftware.arrow-function-snippets

# Diff Checker
https://vscode.one/diff-vscode/#:~:text=There%27s%20two%20primary%20types%20of%20diffs%20you%20can,diff%20panel%20appear%20once%20you%27ve%20completed%20these%20steps%3A