https://learntheweb.courses/topics/html-semantics-cheat-sheet/

# Form

## onSubmit

- Will cause page to reload by defualt
	- Disabled by `event.preventDefault();`
		- See [[Listeners]]


# xmln

- XML Namespaces provide a method to avoid element name conflicts.
- [W3 schools link](https://www.w3schools.com/xml/xml_namespaces.asp)

# Picture

- Useful for two images for different screen size
	- Wrap an image tag with `<picture>`
	- Uses image until media query is met

```html
<picture>
<source
	srcset="/images/image-large"
	media="(min-width: 600px)"
>
	<img src="/images/image-small" />
</picture>
```