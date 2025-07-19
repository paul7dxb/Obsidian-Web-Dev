# OnError

- Display something instead of a broken link

![[Pasted image 20230721100206.png]]

```EJS
<img src="<%= post.imageUrl %>" width="150" alt="User Image not loading" onerror="this.src='https://upload.wikimedia.org/wikipedia/commons/thumb/6/65/No-Image-Placeholder.svg/1665px-No-Image-Placeholder.svg.png'">

```
