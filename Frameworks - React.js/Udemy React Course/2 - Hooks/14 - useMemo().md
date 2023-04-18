- See the requirement for this hook [[12 - React under the hood#React Memo|here]]

```JS
const {items} = props;

const sortedList - useMemo (() => {
	return items.sort((a,b) => a-b )
} , [items]);
```

- Requires props array to be constant and not a reference passed through
- Use memo in parent as well

```JSX
//Empty dependencies array for only one creation at start
const listItems = useMemo(() => [5,3,1,10,9], [])

return(
<ChildComponent items={listItems} />
)
```