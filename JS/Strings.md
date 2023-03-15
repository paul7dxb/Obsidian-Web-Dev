# Methods

## Looping through string

```JS
for (index in s2){
    console.log(s2[index])
}
```

## Conversions

```JS
// num to string
text = num.toString()

// string to num
num = parseInt(text)
```

# indexOf()

```JS
let closeIndex = s.indexOf(")");
```

# lastIndexOf()
```JS
let open = s.substring(0, closeIndex).lastIndexOf("(");
```

# every()

- Loop through each element with given reference
- Use index to get matching element in another array
	- Used in [[Sets Challenges#Check if consistent mapping between two arrays|Sets Challenge]]

```JS
// Arrow function
every((element) => { /* … */ })
every((element, index) => { /* … */ })
every((element, index, array) => { /* … */ })
```

# Slice()

- indexStart INCLUDED
- indexEnd EXCLUDED
```JS
slice(indexStart)
slice(indexStart, indexEnd)

slice(-i) //Last i elements
```