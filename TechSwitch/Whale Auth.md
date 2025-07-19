# Backend

![[Screenshot 2023-09-14 161929.png]]

# Protecting a Route

```c#
    [HttpPost("")]
    [RequiresUserAuth] // Validates Authorization header before entering route
    public IActionResult Create(
        [FromBody] InteractionRequest newInteractionRequest,
        [FromHeader] int UserId // Allows access to UserId in this route
    )
    {
        try
        {
            _interactionService.Create(newInteractionRequest, UserId); // Using UserId from header
            return Ok();
        }
        catch (ArgumentException)
        {
            return Conflict();
        }
    }
```

- use one of the attributes  `[RequiresAdminAuth]` or  `[RequiresUserAuth]`

# UserId
- Accessed using `[FromHeader]` 
- This is the user Id of the authenticated user from the Authorization header
# UserRole
- If admin only then use the `[RequiresAdminAuth]` attribute instead which also checks the role is admin
- In the case of a post edit this wouldn't work as the User of the post can also edit
	- In this case use the  `[RequiresUserAuth]` and then access the role in the route logic from the `UserRole` header (as seen in the above image)


# Frontend

- Protected routes require the Authorization header
- After a user logs in the required header value is stored in the `LoginManager` context

# Check user is logged in


# Using the Auth header from the context


