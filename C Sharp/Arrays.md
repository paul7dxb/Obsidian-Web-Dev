```c#
//Reverse array
Array.reverse(myArray)
```

  
### Array  

# Initialise array  
```c#
string[] answers = new string[4];  
```  

  - Array cannot change size  

```  c#
int[] oddNumber = {1,3,5,7}  
//Can reassign  
oddNumbers[2] = 5;  
```  

# Array.IndexOf()

```c#
Array.IndexOf(myArray,"elementValue");
```

# Array.Aggregate()

```c#
using System.Linq;

// Number work
// Multiply elements of an array
int[] x
x.Aggregate((a,b) => a*b);

// Get longest string in array
string[] fruits = { "apple", "mango", "orange", "passionfruit", "grape" };

// Determine whether any string in the array is longer than "banana".
string longestName =
    fruits.Aggregate("banana",
                    (longest, next) =>
                        next.Length > longest.Length ? next : longest,
    // Return the final result as an upper case string.
                    fruit => fruit.ToUpper());

Console.WriteLine(
    "The fruit with the longest name is {0}.",
    longestName);
```

# Minimum Value Array

```c#
using System.Linq;

return myArr.Min();

public static int FindSmallestInt(int[] args) => args.Min();
```