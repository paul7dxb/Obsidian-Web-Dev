# String.format()

```c#
//Number refers to replacement strings. Can reuse numbers
string myString = String.format("{0} {1}", "First", "Second")

// Currency
string myString = String.format("{0:C}", "123.45")

// Decimal and comma formatting
string myString = String.format("{0:N}", "123.45")

// Percentage
string myString = String.format("Percentage: {0:P}", "0.45")

// Custom Format
// Formatting works R-L so extra digits will be in the (###)
string myString = String.format("Phone number {0:(###) ###-####}", "1234567890")
```

# String Methods

```C#
string myString = "Some text here"

myString = myString.Substring(start,end)
myString = myString.ToUpper();
myString = myString.Replace(" ", "--")
myString = myString.Remove(start,end)
myString = myString.Trim() //Get rid of beginneg / ending spaces
```