- Setting fallback to false will stop pages for static routes being generated in production
	- Going to a new post page will give a 404 error

# Blocking

- Tells NextJS the list of paths is not exhaustive
	- Will not respond with 4040 error immediately
	- Can generate on demand and then caches

- With true
	- Return empty page then pull content
- Blocking
	- USer doesnt see anything until page is rendered and is then served