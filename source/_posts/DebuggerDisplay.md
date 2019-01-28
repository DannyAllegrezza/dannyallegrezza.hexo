---
title: DotNet Tips - The DebuggerDisplay() attribute
date: 2017-10-09 11:01:40
tags: [C#, tips]
categories: Code
thumbnail: /images/thumbnails/debugger.JPG
---
Debugging is one of the most crucial skills that a software developer can possess. I want to share a tip I recently learned while watching a great [Pluralsight course](https://app.pluralsight.com/library/courses/csharp-tips-traps/table-of-contents). When debugging your C# code, wouldn't it be nice to know some interesting data about the giant collection of objects you are hovering over? 

That is where the `DebuggerDisplay()` attribute steps in!

<!-- more -->

To quote the excellent [MSDN docs](https://docs.microsoft.com/en-us/dotnet/framework/debug-trace-profile/enhancing-debugging-with-the-debugger-display-attributes):

> Debugger display attributes allow the developer of the type, who specifies and best understands the runtime behavior of that type, to also specify what that type will look like when it is displayed in a debugger. 

## How to use the `DebuggerDisplay()` attribute
Let's assume we have a simple `Person` class who is not using the DebuggerDisplay functionality.

```csharp
public class PersonWithoutDebuggerDisplay
{
    public string Name { get; set; }
    public int AgeInYears { get; set; }

    public PersonWithoutDebuggerDisplay(string name, int years)
    {
        Name = name;
        AgeInYears = years;
    }
}
```

1. Add using statement for `System.Diagnostics`.
2. Decorate your class or property with the `[DebuggerDisplay("")]` attribute. Inside the quotation marks you can write your own custom message which will override the default message, which simply displays either your types information or the `ToString()` override if one is present.

For example: 

```csharp
[DebuggerDisplay("This person is named {Name} and is {AgeInYears} old")]
public class PersonWithoutDebuggerDisplay
{
    public string Name { get; set; }
    public int AgeInYears { get; set; }

    public PersonWithoutDebuggerDisplay(string name, int years)
    {
        Name = name;
        AgeInYears = years;
    }
}
```

{% asset_img debugger.JPG Notice the fancy message, nice! %}

To me, this could definitely help save me some extra clicks and would be helpful when working with a large collection of complex data.

### Considerations

* There will be overhead for this operation
* If we name our properties well, we shouldn't need to use this

What are your thoughts on the `DebuggerDisplayAttribute`? 