### What's Configuration Path

A <strong> configuration path</strong> is a **string** separate from a delimiter. The default delimiter in ASP.NET Core Configuration is ":".

See the code [here](https://github.com/aspnet/Configuration/blob/dev/src/Microsoft.Extensions.Configuration.Abstractions/ConfigurationPath.cs#L17):
```C#
public static readonly string KeyDelimiter = ":";
```

### Methods
#### 1. Combine(...): Combines the segments string into a path string using delimiter.
```C#
public static string Combine(params string[] pathSegments)
public static string Combine(IEnumerable<string> pathSegments)
```

Examples:
```C#
string path1 = ConfigurationPath.Combine("a", "b", "c"); // path1 == "a:b:c"

IList<string> segments = new List<string> { "x", "y", "z" };
string path2 = ConfigurationPath.Combine(segments); // path2 == "x:y:z"

```

#### 2. GetSectionKey(...): extracts the last path segment from the path.
```C#
public static string GetSectionKey(string path)
```

Examples:
```C#
string section1 = ConfigurationPath.GetSectionKey(path1); // section1 == "c"
string section2 = ConfigurationPath.GetSectionKey(path2); // section2 == "z"
```

#### 3. GetParentPath(...): extracts the the path corresponding to the parent node from the path.
```C#
public static string GetParentPath(string path)
```

Examples:
```C#
string parent1 = ConfigurationPath.GetParentPath(path1); // parent1 == "a:b"
string parent2 = ConfigurationPath.GetParentPath(path2); // parent2 == "x:y"

string parent3 = ConfigurationPath.GetParentPath(ConfigurationPath.GetParentPath(path1)); // parent3 == "a"
```

