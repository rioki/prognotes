
# C# Cheat Sheet

## Types

The following basic types in C# exist:

* `bool` a boolean (true or false)
* `char` a single character
* `int` an integer number
* `float` a floating point number aka real number
* `double` a double float, like float just more precision
* `string` a text, made up of `char`s

## Conditions

Often you need to do something only under certain conditions, for that
you use the `if`, `if/else` or `switch` construct.

### If Statement

A simple condition can be tested and it's code executed like follows:

```csharp
// int n;
if (n % 3 == 0)
{
    Console.WriteLine("Fizz");
}
```

Often you need to have an either / or construction:

```csharp
// int n;
if (n % 3 == 0)
{
    Console.WriteLine("Fizz");
}
else 
{
    Console.WriteLine("{0}", n);
}
```

If you have more than 2 conditions to handle you cam chain if to an else clause
as many times are you like:

```csharp
// int n;
if (n % 3 == 0 && n % 5 == 0)
{
    Console.WriteLine("FizzBuzz");
}
else if (n % 3 == 0)
{
    Console.WriteLine("Fizz");
}
else if (n % 5 == 0)
{
    Console.WriteLine("Buzz");
}
else
{
    Console.WriteLine("{0}", n);
}
```

**Note:** The conditions are evaluate from top to bottom, the first that is true 
will trigger it's code and skip the rest.

You may obviously nest conditions are much as you like:

```csharp
// int n;
if (n % 3 == 0)
{
    if (n % 5 == 0)
    {
        Console.WriteLine("FizzBuzz");
    }
    else
    {
        Console.WriteLine("Fizz");
    }
}
else
{
    if (n % 5 == 0)
    {
        Console.WriteLine("Buzz");
    }
    else
    {
        Console.WriteLine("{0}", n);
    }
}
```

### Logic Operators

An `if` statement contains a truth value. But often you need to combine multiple 
truth values into one statement. To do this you use local operators:

* `&&` and
* `||` or
* `!` not

You can and in some cases you must use braces [ `(` and `)` ] to group clauses 
together. For example:

```csharp
if ((type == "apple" && color == "red") || color == "green")
{
    return "All red apples or green fruit.";
}

if (type == "apple" && (color == "red" || color == "green"))
{
    return "Only apples that are red or green.";
}

if (type == "apple" && !(color == "red" || color == "green"))
{
    return "Only apples that are not red or green.";
}
```

### Switch Statement

If you have multiple options and they can be hardcoded a `switch` statement can 
be used instead of a `if/else` cascade.

```csharp
// int shipSize;
switch (shipSize)
{
    case 1:
        type = "Submarine";
        break;
    case 2:
        type = "Frigatte";
        break;
    case 2:
        type = "Destroyer";
        break;
    case 4:
        type = "Aircraft Carrier";
        break;
    default:
        type = "Invalid Ship";
        break;
}
```

You don not need to specify every possible option. If you have a default case,
all not specified options go there. Having a default is also optional; then 
nothing happens for the unspecified cases.

## Loops

Often you want to do a thing multiple times, often for every element in a list.
For that you have the options to loop with `foreach`, `for`, `while` and `do/while`.

### Foreach Loops

The simples loop to use, when you have a list (or any object that implement IEnumerable)
you can use the `foreach` loop.

```csharp
// List<int> numbers;
foreach (int number in numbers)
{
    if (number % 2 == 0)
    {
        Console.WriteLine("{0} is even", number);
    }
    else
    {
        Console.WriteLine("{0} is odd", number);
    }
}
```

### For Loops

The `for` loop is like the `foreach` loop, but it can use custom start and
end conditions. Generally you use `for` instead of `foreach` when you need
the current index. 

```csharp
// List<int> numbers;
for (int i = 0; i < numbers.Count; i++)
{
    if (numbers[i] % 2 == 0)
    {
        Console.WriteLine("{0}: {1} is even", i, numbers[i]);
    }
    else
    {
        Console.WriteLine("{0}: {1} is odd", i, numbers[i]);
    }
}
```

**Note:** What you write in the slots for init, end condition and increment can
be totally arbitrary; we just tend to use this pattern since almost all loops
are over lists or ranges of numbers.

### While Loops

A `while` loop is even more flexile. It allows you to continue executing until 
a given condition is met.

```csharp
// List<int> numbers;
int i = 0;
while (i < numbers.Count)
{
    if (numbers[i] % 2 == 0)
    {
        Console.WriteLine("{0}: {1} is even", i, numbers[i]);
    }
    else
    {
        Console.WriteLine("{0}: {1} is odd", i, numbers[i]);
    }
    i++;
}
```

### Do/While Loops

The `do/while` loop is like the `while` loop, but the check to terminate the 
loop it at the end of the loop execution not before, this means that the 
loop will execute at least once.

```csharp
// List<int> numbers;
if (numbers.Count > 0)
{
    int i = 0;
    do
    {
        if (numbers[i] % 2 == 0)
        {
            Console.WriteLine("{0}: {1} is even", i, numbers[i]);
        }
        else
        {
            Console.WriteLine("{0}: {1} is odd", i, numbers[i]);
        }
        i++;
    }
    while (i < numbers.Count);
}
```

### Loop Control

While this is discouraged, manipulate loop execution with the `break` and 
`continue` keywords.

```csharp
for (int i = 0; i < 10; i++) 
{
  if (i == 4) 
  {
    break;
  }
  Console.WriteLine(i);
}
```

The above code just counts to 3 instead of 10. As the `break` keyword will end 
the loop execution and continue after the loop. A good place where break may be 
used is when you are looking for an item and found it.

```csharp
for (int i = 0; i < 10; i++) 
{
  if (i == 4) 
  {
    continue;
  }
  Console.WriteLine(i);
}
```

The above code will skip the 4. The `continue` keyword instruct the code to skip
this loop iteration. A common example is if you do something complicated to 
objects, but only under certain conditions. You would then check the condition
and `continue`.

## Objects

Object comme in two flavors `struct` and `class`. At a bastic level they are
the same thing; just they have different default visibility and communicate 
programmer intent.

### Struct as Data Container

Generally structs are used as containers to group associated values together.

```csharp
public struct Person
{
    string Name;
    int Age;
    string Address;
};
```

### Classes as Behavioral Pattern

While classes also contain data, they are generally more defined on their behavior.

> *An object is data and functions.*

```csharp
public class AddressBook
{
    private List<Person> entries;

    public int Count 
    {
        get { return entries.Count };
    }

    public void Add(Person person)
    {
        entries.Add(person);
    }

    public Person FindByName(string name)
    {
        foreach (Person person in entries)
        {
            if (person.Name == name)
            {
                return person;
            }
        }
        return null;
    }
};
```

### Functions

In C# functions must be associated to a class. In the above example `Add` and
`FindByName` are functions.

### Properties

In C# you can have properties. The look like class variable, but actually are 
hidden functions. In the above example `Count` is such a property and it forwards 
the list's Count. 

But you can also have a set function like such:

```csharp
public class TimePeriod
{
    private double _seconds;

    public double Hours
    {
        get { return _seconds / 3600; }
        set
        {
            if (value < 0 || value > 24)
            {
                throw new ArgumentOutOfRangeException(nameof(value), 
                            "The valid range is between 0 and 24.");
            }

            _seconds = value * 3600;
        }
    }
}
```

### Constructor

```csharp
public class Vector3
{
    public double X;
    public double Y;
    public double Z;

    public Vector3()
    {
        X = 0.0;
        Y = 0.0;
        Z = 0.0;
    } 

    public Vector3(double x, double y, double z)
    {
        X = x;
        Y = y;
        Z = z;
    } 

    public double Length
    {
        get { return Math.Sqrt(X*X + Y*Y + Z*Z); }
    }
}
```

```csharp
Vector3 defaultVector = new Vector3();
Vector3 initVector = new Vector3(1.0, 2.0, 3.0);
```

### Static Functions

In C# a function must be on a class. Often we want to have functions that don't 
have an associated object. So we use a static function. 

```csharp
public class VectorMath
{
    public static double AverageLength(List<Vector3> vectors)
    {
        double totalLength = 0.0;
        foreach (Vector3 vector in vectors)
        {
            totalLength += vector.Length;
        }
        return totalLength / vectors.Count;
    }
};
```

### Visibility

For classes (and structs) we control what we want external code to use and 
what we don't want external code to use. For example we want to hide certain 
implementation details. This is primarily done, since things that other code 
uses needs to be stable and never change, but internals we can change when ever 
we want.

Although there are more, we use the following classifiers

* `public`: these bits should be used by other code
* `private`: these bits should be used only by this class

## Algorithms

### Numerical Algorithms

```csharp
public class Numeric
{
    public static double Sum(List<double> values)
    {
        double result = 0.0;
        foreach (double value in values)
        {
            result += value;
        }
        return result;
    }

    public static double Average(List<double> values)
    {
        double result = 0.0;
        foreach (double value in values)
        {
            result += value;
        }
        return result / values.Count;
    }

    public static double Max(List<double> values)
    {
        double result = Double.MinValue;
        foreach (double value in values)
        {
            if (value > result)
            {
                result = value;
            }
        }
        return result;
    }

    public static double Min(List<double> values)
    {
        double result = Double.MaxValue;
        foreach (double value in values)
        {
            if (value < result)
            {
                result = value;
            }
        }
        return result;
    }
}
```

### List Manipulation

```csharp
public struct Widget
{
    int Value;
};

public class ListEditor
{
    public static Widget FirstOf(List<Widget> widgets, int value)
    {
        foreach (Widget widget in widgets)
        {
            if (widget.Value == value)
            {
                return widget;
            }
        }
        return null;
    }

    public static List<Widget> AllOf(List<Widget> widgets, int value)
    {
        List<Widget> result;
        foreach (Widget widget in widgets)
        {
            if (widget.Value == value)
            {
                result.Add(widget);
            }
        }
        return result;
    }

    public static List<Widget> EveryNthElement(List<Widget> widgets, int n)
    {
        List<Widget> result;
        for (int i = 0; i < widgets.Count; i++)
        {
            if (i % n == 0)
            {
                result.Add(widgets[i]);
            }
        }
        return result;
    }
}
```

### File Operations

```csharp
public class FileOperations
{
    public static List<string> ReadLineByLine(string path)
    {
        List<string> result;

        StreamReader reader = new StreamReader(path);

        string line;
        do
        {
            line = reader.ReadLine();
            if (line != null)
            {
                result.Add(line);
            }
        }
        while (line != null);

        return result;
    }

    public static void WriteLineByLine(string path, List<string> lines)
    {
        StreamWriter output = new StreamWriter(path);
        foreach (string line in lines)
        {
            writer.WriteLine(line);
        }
    }
}
```