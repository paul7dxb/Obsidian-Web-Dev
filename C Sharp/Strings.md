# String.format()

```c#
// string interpolation
string name = "myName";
$"Hello, {name} how are you doing today?";

// Number refers to replacement strings. Can reuse numbers
string myString = String.format("{0} {1}", "First", "Second");

// Currency
string myString = String.format("{0:C}", "123.45");

// Decimal and comma formatting
string myString = String.format("{0:N}", "123.45");

// Percentage
string myString = String.format("Percentage: {0:P}", "0.45");

// Custom Format
// Formatting works R-L so extra digits will be in the (###)
string myString = String.format("Phone number {0:(###) ###-####}", "1234567890");
```

# String Methods

```C#
string myString = "Some text here"

string[] subs = s.Split(' ');

myString = myString.Substring(start,end)
myString = myString.ToUpper();
myString = myString.Replace(" ", "--")
myString = myString.Remove(start,end)
myString = myString.Trim() //Get rid of beginneg / ending spaces
```

# Edit string of words

```c#
return String.Join(" ", phrase.Split().Select(i => Char.ToUpper(i[0]) + i.Substring(1)));
```

|String Functions|Definitions|
|---|---|
|`Clone()`|Make clone of string.|
|`CompareTo()`|Compare two strings and returns integer value as output. It returns 0 for true and 1 for false.|
|`Contains()`|The C# Contains method checks whether specified character or string is exists or not in the string value.|
|`EndsWith()`|This EndsWith Method checks whether specified (character/string) is the last (character/string) of string or not.|
|`Equals()`|The Equals Method in C# compares two string and returns Boolean value as output.|
|`GetHashCode()`|This method returns HashValue of specified string.|
|`GetType()`|It returns the System.Type of current instance.|
|`GetTypeCode()`|It returns the Stystem.TypeCode for class System.String.|
|`IndexOf()`|Returns the index position of first occurrence of specified character.|
|`ToLower()`|Converts String into lower case based on rules of the current culture.|
|`ToUpper()`|Converts String into Upper case based on rules of the current culture.|
|`Insert()`|Insert the string or character in the string at the specified position.|
|`IsNormalized()`|This method checks whether this string is in Unicode normalization form C.|
|`LastIndexOf()`|Returns the index position of last occurrence of specified character.|
|`Length`|It is a string property that returns length of string.|
|`Remove()`|This method deletes all the characters from beginning to specified index position.|
|`Replace()`|This method replaces the character.|
|`Split()`|This method splits the string based on specified value.|
|`StartsWith()`|It checks whether the first character of string is same as specified character.|
|`Substring()`|This method returns substring.|
|`ToCharArray()`|Converts string into char array.|
|`Trim()`|It removes extra whitespaces from beginning and ending of string.|

