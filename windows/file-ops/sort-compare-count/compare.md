# Compare

<mark style="color:yellow;">`Compare-Object`</mark>

3 Important Parameters:

<mark style="color:yellow;">`-ReferenceObject`</mark> The ReferenceObject is the baseline.

<mark style="color:yellow;">`-DifferenceObject`</mark> The DifferenceObject is what you are looking for differences in.

<mark style="color:yellow;">`-Property`</mark> This is the property of the object that you are comparing. Can be a comma-seperated list?

<mark style="color:yellow;">`<=`</mark> Indicates that the property is present only on the ReferenceObject (Left Side).

<mark style="color:yellow;">`=>`</mark> Indicates that the property is present only on the DifferenceObject (Right Side).

Compares two files and displays the differences using the File Compare command in CMD.

```powershell
fc C:\path\to\file1.txt C:\path\to\file2.txt
```

Compares the contents of two files or sets of files byte-by-byte, using the Comp command.

```powershell
comp C:\path\to\file1.txt C:\path\to\file2.txt
```

Compares two files and shows differences using PowerShell. This command reads each file's content and then compares the objects.

{% code overflow="wrap" %}
```powershell
Compare-Object (Get-Content C:\path\to\file1.txt) (Get-Content C:\path\to\file2.txt)
```
{% endcode %}

Checks if two files are identical, returning True or False, using PowerShell.

```powershell
(Get-Content C:\path\to\file1.txt) -eq (Get-Content C:\path\to\file2.txt)
```

An alias in PowerShell for Compare-Object, used to compare file contents similar to the Unix/Linux <mark style="color:yellow;">`diff`</mark> command.

Note: <mark style="color:yellow;">`diff`</mark> as an alias may not be available in all PowerShell environments by default.

```powershell
diff (Get-Content C:\path\to\file1.txt) (Get-Content C:\path\to\file2.txt)
```

Example: Comparing two text Files

{% code overflow="wrap" %}
```powershell
Compare-Object -ReferenceObject (get-content .\testing.txt) -DifferenceObject (get-content .\2testing.txt)
```
{% endcode %}

Example: Comparing the Process List of two computers:

Collect the baseline computer's process list:

```powershell
Get-Process | Export-CliXML reference.xml
```

Move it to the other computer to compare:

{% code overflow="wrap" %}
```powershell
Compare-Object -Reference (Import-Clixml reference.xml) -Difference (Get-Process) -Property Name
```
{% endcode %}
