---
tags:  CSharp
---

# How to get C# const names and values using reflection

You have a `static` class that you only use to store some constants, and you want to get all the values stored within the class.

```cs
public static class Instances
{
 public const string LeagueMen = "league_men";
 public const string LeagueWomen = "league_women";
}
```

You can get the list of the const names and the related values using reflection.

First, you have to get the full list of field info:

```cs
FieldInfo[] fieldInfos = typeof(Instances)
  .GetFields(BindingFlags.Public | BindingFlags.Static | BindingFlags.FlattenHierarchy);
```

Notice the `typeof(Instances)`: you must pass the type you want to explore.

Now you can get the names:

```cs
string[] allNames = fieldInfos
  .Select(i => i.Name)
  .ToArray(); // [LeagueMen, LeagueWomen]
```

And you can also get the related values:

```cs
string[] allValues = fieldInfos
  .Select(i => i.GetValue(i).ToString())
  .ToArray(); // [league_men, league_women]
```

Now you can use this method to validate an input:

```cs
string instance = "league_women";

var allInstances = GetSupportedInstances();

if (!allInstances.Contains(instance))
{
    throw new ArgumentException($"{instance} is not supported");
}

    private static string[] GetSupportedInstances()
    {
        var fieldInfos = typeof(Instances)
          .GetFields(BindingFlags.Public | BindingFlags.Static | BindingFlags.FlattenHierarchy);

        return fieldInfos
          .Select(i => i.GetValue(i).ToString())
          .ToArray();
    }

```
