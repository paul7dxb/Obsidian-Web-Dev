- Prevent reaching routes even by typing in the url manually
- Use a loader to see if user has a token

- Return null at end of if statements to catch cases where none of the if conditions are met

```JS
    export function checkAuthLoader() {
      // this function will be added in the next lecture
      // make sure it looks like this in the end
      const token = getAuthToken();
      
      if (!token) {
        return redirect('/auth');
      }
     
      return null;
    }
```