# C# Cheatsheet
- https://hackr.io/blog/c-sharp-cheat-sheet

# For Loop

```c#
for (int i=0; i<10; i++) { }
```
## foreach
```c
foreach (int value in list)
```

Using and to control loop behaviour break continue

## For Loop Two variables
```c#
for(int i = BinaryArray.Length - 1, p = 0; i > -1; i--, p++) {
	if (BinaryArray[i] > 0) sum += (int)Math.Pow(2, p);
} 
```
# Creating arrays
```c#
new int[4] new int[] {1,2,3,4}

//Creat array of size
int[] numbers = new int[variableCount];
```

Accessing arrays using array[2]

# String to character array
```c#
string sentence = "Example sentence";  
char[] charArr = sentence.ToCharArray(); 
```

# Write to console
```c#
Console.WriteLine("Text for console");
Console.Write("Text for console");

Console.clear()
```

# While

```c#
while () {
	//...
}
```

## Do While

- Executed at least once
```c#
do {

} while();
```
# Class Instance
```c#
MyClass instanceName = new MyClass()
```

# Switch

```c#
string result;
        
switch(current)
{
  case "green": result = "yellow"; break;
  case "yellow": result = "red"; break;
  case "red": result = "green"; break;
  default:
	throw new ArgumentException($"{nameof(current)} is not a valid traffic light state.");
}

return result;
```

# Dictionary

```c#
new Dictionary<string, string>{ {"green","yellow"}, {"yellow","red"}, {"red","green"} }
```

# ForEach
```
foreach(var fruit in fruits){
	
}
```