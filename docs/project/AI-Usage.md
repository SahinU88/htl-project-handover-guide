# Usage of AI

Describe **how and for what** you used AI tools (e.g. ChatGPT, GitHub Copilot, Claude, ...)
during your project. Be honest. Using AI is allowed, but you should be able to explain
what the AI produced and why you accepted, changed or rejected it.

Aim for about **1-2 pages (A4)**.

Please cover at least:

- **Which AI tools** did you use? (name + version if known)
- **For what** did you use them? (e.g. generating code, explaining errors, writing
  documentation, brainstorming ideas, refactoring, learning a new concept, ...)
- **How did it help** and where did it **not** help or produce wrong results?
- **1-2 concrete examples** with, if possible: the **prompt** you used, the **output** you
  got, and the **final code/solution** you actually used (and what you changed).

---

## Example

> Short, filled-in example for a C# WPF application. Replace it with your own.

### Where we used AI

- **GitHub Copilot**: autocompletion while writing C# code.
- **ChatGPT**: explaining error messages and generating a first draft for the CSV reading logic.

We used AI mainly to **get started faster** and to **understand errors**. We always read the
generated code and tested it before keeping it. In a few cases the AI suggested code that did
not compile or used a library we did not have, so we had to adjust it.

### Example 1: Reading a CSV file

**Prompt:**

> "Write a C# method that reads a CSV file `customers.csv` with the columns
> `Id;Name;Email` (separated by semicolons) and returns a list of Customer objects.
> The first line is a header."

**Output (shortened):**

```csharp
public List<Customer> ReadCustomers(string path)
{
    var customers = new List<Customer>();
    var lines = File.ReadAllLines(path);
    foreach (var line in lines.Skip(1)) // skip header
    {
        var parts = line.Split(',');
        customers.Add(new Customer {
            Id = int.Parse(parts[0]),
            Name = parts[1],
            Email = parts[2]
        });
    }
    return customers;
}
```

**What we changed / final solution:**

The output used a comma (`,`) as separator, but our file uses a semicolon (`;`). We also
added a check for empty lines so the app does not crash on a trailing blank line:

```csharp
public List<Customer> ReadCustomers(string path)
{
    var customers = new List<Customer>();
    foreach (var line in File.ReadAllLines(path).Skip(1))
    {
        if (string.IsNullOrWhiteSpace(line)) continue; // ignore empty lines
        var parts = line.Split(';');                   // our file uses ';'
        customers.Add(new Customer {
            Id = int.Parse(parts[0]),
            Name = parts[1],
            Email = parts[2]
        });
    }
    return customers;
}
```

**Conclusion:** The AI gave us a good starting point, but we had to understand the code to
spot the wrong separator and to make it robust against empty lines.

### Example 2: Explaining an error (optional second example)

Briefly show a case where you pasted an error message and the AI helped you understand or
fix it. Include the prompt, the key part of the answer, and what you did with it.

---

[Back to the overview](./../../README.md)
