# Scripting

## <mark style="color:red;">PowerShell</mark>

### <mark style="color:purple;">ForEach-Object</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ForEach-Object { $_ }</code></mark></td><td>Takes each item on the pipeline and handles it as $_</td></tr><tr><td><mark style="color:yellow;">`[cmdlet]</mark></td><td>% { [cmdlet] $_ }`</td></tr><tr><td><mark style="color:yellow;"><code>Get-Content C:\path\to\file.txt | ForEach-Object { $_.ToUpper() }</code></mark></td><td>Converts all text in a file to uppercase.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Content C:\path\to\file.txt | ForEach-Object { $_.Trim() }</code></mark></td><td>Trims whitespace from the start and end of each line in a file.</td></tr></tbody></table>

Processes each line in a file and outputs to a new file. Customize the <mark style="color:yellow;">`do`</mark> command for specific modifications:

```powershell
for /f "tokens=*" %i in (C:\path\to\file.txt) do @echo %i
```

### <mark style="color:purple;">Where-Object</mark>

Where-Object condition (alias where or ?):

```powershell
Get-Process | Where-Object {$_.name -eq "notepad"}
```

### <mark style="color:purple;">Loops</mark>

#### <mark style="color:green;">Do Loop</mark>

Do-While Loop

```powershell
$counter = 1
do {
    Write-Host "Do-While Loop Iteration: $counter"
    $counter++
} while ($counter -le 5)
```

Do-Until Loop

```powershell
$counter = 1
do {
    Write-Host "Do-Until Loop Iteration: $counter"
    $counter++
} until ($counter -gt 5)
```

Do-While Loop with Condition at the End

```powershell
$counter = 1
do {
    Write-Host "Do-While Loop (Condition at the End) Iteration: $counter"
    $counter++
} while ($counter -le 5)
```

Do-Until Loop with Condition at the End

```powershell
$counter = 1
do {
    Write-Host "Do-Until Loop (Condition at the End) Iteration: $counter"
    $counter++
} until ($counter -gt 5)
```

Do-While Loop with Break

```powershell
$counter = 1
do {
    Write-Host "Do-While Loop with Break Iteration: $counter"
    $counter++
    if ($counter -eq 3) {
        Write-Host "Breaking out of the loop"
        break
    }
} while ($true)
```

#### <mark style="color:green;">For Loop</mark>

Basic For Loop

```powershell
for ($i = 1; $i -le 5; $i++) {
    Write-Host "Iteration $i"
}
```

For Loop with Array

```powershell
$fruits = @("Apple", "Banana", "Cherry", "Date")
for ($i = 0; $i -lt $fruits.Length; $i++) {
    Write-Host "Fruit: $($fruits[$i])"
}
```

ForEach Loop (For Each Element in an Array)

```powershell
$colors = @("Red", "Green", "Blue", "Yellow")
foreach ($color in $colors) {
    Write-Host "Color: $color"
}
```

ForEach Loop (For Each Item in a Directory)

```powershell
$files = Get-ChildItem -Path C:\YourDirectoryPath
foreach ($file in $files) {
    Write-Host "File Name: $($file.Name)"
}
```

ForEach-Object Loop (Pipeline)

```powershell
$numbers = 1..5
$numbers | ForEach-Object {
    Write-Host "Number: $_"
}
```

ForEach Loop (Associative Array/HashTable)

```powershell
$person = @{
    "Name" = "John";
    "Age" = 30;
    "City" = "New York";
}
foreach ($key in $person.Keys) {
    Write-Host "$key: $($person[$key])"
}
```

#### <mark style="color:green;">Foreach Loop</mark>

```powershell
$letterArray = "a","b","c","d"
foreach ($letter in $letterArray)
{
  Write-Host $letter
}
```

Example 1: ForEach Loop (For Each Element in an Array)

```powershell
$fruits = @("Apple", "Banana", "Cherry", "Date")
ForEach ($fruit in $fruits) {
    Write-Host "Fruit: $fruit"
}
```

Example 2: ForEach Loop (For Each Element in a Range)

```powershell
$numbers = 1..5
ForEach ($number in $numbers) {
    Write-Host "Number: $number"
}
```

Example 3: ForEach Loop (For Each Item in a Directory)

```powershell
$files = Get-ChildItem -Path C:\YourDirectoryPath
ForEach ($file in $files) {
    Write-Host "File Name: $($file.Name)"
}
```

Example 4: ForEach Loop (For Each Key-Value Pair in a Hashtable)

```powershell
$person = @{
    "Name" = "John";
    "Age" = 30;
    "City" = "New York";
}
ForEach ($key in $person.Keys) {
    Write-Host "$key: $($person[$key])"
}
```

Example 5: ForEach-Object Loop (For Each Object in a Pipeline)

```powershell
$colors = @("Red", "Green", "Blue", "Yellow")
$colors | ForEach-Object {
    Write-Host "Color: $_"
}
```

#### <mark style="color:green;">While Loop</mark>

while (){}

Example 1: Basic While Loop

```powershell
$counter = 1
while ($counter -le 5) {
    Write-Host "While Loop Iteration: $counter"
    $counter++
}
```

Example 2: While Loop with User Input

```powershell
$continue = $true
while ($continue) {
    $input = Read-Host "Do you want to continue? (Y/N)"
    if ($input -eq "N" -or $input -eq "n") {
        $continue = $false
    }
}
```

Example 3: Infinite While Loop with Break

```powershell
$counter = 1
while ($true) {
    Write-Host "Infinite While Loop Iteration: $counter"
    $counter++
    if ($counter -gt 5) {
        Write-Host "Breaking out of the loop"
        break
    }
}
```

### <mark style="color:purple;">Conditions</mark>

```powershell
if (<test1>)
    {<statement list 1>}
[elseif (<test2>)
    {<statement list 2>}]
[else
    {<statement list 3>}]
```

Example 1: While Loop with a Condition

```powershell
$counter = 1
while ($counter -le 5) {
    Write-Host "While Loop Iteration: $counter"
    $counter++
}
```

Example 2: Do-While Loop

```powershell
$counter = 1
do {
    Write-Host "Do-While Loop Iteration: $counter"
    $counter++
} while ($counter -le 5)
```

Example 3: While Loop with User Input

```powershell
$continue = $true
while ($continue) {
    $input = Read-Host "Do you want to continue? (Y/N)"
    if ($input -eq "N" -or $input -eq "n") {
        $continue = $false
    }
}
```

Example 4: Do-While Loop with User Input

```powershell
$continue = $true
do {
    $input = Read-Host "Do you want to continue? (Y/N)"
    if ($input -eq "N" -or $input -eq "n") {
        $continue = $false
    }
} while ($continue)
```

Example 5: While Loop with a Break Condition

```powershell
$counter = 1
while ($true) {
    Write-Host "While Loop Iteration: $counter"
    $counter++
    if ($counter -gt 5) {
        Write-Host "Breaking out of the loop"
        break
    }
}
```

### <mark style="color:purple;">Generating Ranges</mark>

Echo "Hello!" 10 times.

```powershell
1..10 | % {echo "Hello!"}`
```

Generate a range of numbers in reverse order from 10 to 1

```powershell
$range = 10..1
$range
```

Generate a range of letters from 'A' to 'Z'

```powershell
$range = 'A'..'Z'
$range
```

Generate a range of even numbers from 2 to 10 with a step size of 2

```powershell
$range = 2..10 | Where-Object { $_ % 2 -eq 0 }
$range
```

Generate a range of numbers based on variables

```powershell
$start = 5
$end = 15
$range = $start..$end
$range
```

### <mark style="color:purple;">Properties</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Get-Process | Get-Member</code></mark></td><td>Gives the methods and properties of the object/cmdlet.</td></tr><tr><td><mark style="color:yellow;"><code>(cmdlet).property</code></mark></td><td>Command Structure.</td></tr><tr><td><mark style="color:yellow;"><code>(GetProcess).Name</code></mark></td><td>Returns the single property of 'name' of every process.</td></tr><tr><td><mark style="color:yellow;"><code>-ExpandProperty</code></mark></td><td>Extracts values from properties.</td></tr></tbody></table>

### <mark style="color:purple;">Functions</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Get-Help about_Functions</code></mark></td><td>Displays the help about functions</td></tr><tr><td><mark style="color:yellow;"><code>Get-Help about_Functions_Advanced</code></mark></td><td>Displays some more in-depth help about functions</td></tr><tr><td><mark style="color:yellow;"><code>Function Do-Stuff { Get-Date; Get-Process; Get-Service }</code></mark></td><td>Creates a function</td></tr><tr><td><mark style="color:yellow;"><code>Do-Stuff</code></mark></td><td>Runs the function</td></tr></tbody></table>

### <mark style="color:purple;">Comments</mark>

Creates a comment beside cmdlet:

```powershell
Get-Process # comment
```

Multi-line comment:

```powershell
<# comment
|
|
comment #>
```

### <mark style="color:purple;">How to find the data type</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>$PSHome | Get-Member</code></mark></td><td>Displays System.String with its objects and properties.</td></tr><tr><td><mark style="color:yellow;"><code>$A=12</code></mark></td><td>Creates variable A with an integer value of 12.</td></tr><tr><td><mark style="color:yellow;"><code>$A | Get-Member</code></mark></td><td>Displays System.Int32 with its objects and properties.</td></tr></tbody></table>

## <mark style="color:red;">CMD</mark>

Delete all .txt files in the current directory older than 7 days:

```powershell
forfiles /s /m *.txt /d -7 /c "cmd /c del @file"
```

Delete files older than 30 days in a specific directory

```powershell
forfiles /p "C:\path\to\directory" /s /m *.* /d -30 /c "cmd /c del @file"
```

<mark style="color:yellow;">`/s`</mark>: Recurse into subdirectories.

<mark style="color:yellow;">`/m *.txt`</mark>: Include only files with the .txt extension.

<mark style="color:yellow;">`/d -7`</mark>: Include files that are older than 7 days (negative value signifies "older than").

<mark style="color:yellow;">`/c "cmd /c del @file"`</mark>: Execute the del @file command for each matching file.

Move all files newer than yesterday from the C:\Temp folder to the D:\Archive folder:

```powershell
forfiles /s /m * /d +1 /c "cmd /c move @file D:\Archive"
```

<mark style="color:yellow;">`/s`</mark>: Recurse into subdirectories.

<mark style="color:yellow;">`/m *`</mark>: Include all files (regardless of extension).

<mark style="color:yellow;">`/d +1`</mark>: Include files that are newer than yesterday (positive value signifies "newer than").

<mark style="color:yellow;">`/c "cmd /c move @file D:\Archive"`</mark>: Execute the move @file D:\Archive command for each matching file.

Copy all .jpg files from the C:\Photos folder to the D:\Backup folder:

```powershell
forfiles /s /m *.jpg /c "cmd /c copy @file D:\Backup"
```

Copy all PDF files from one directory to another

{% code overflow="wrap" %}
```powershell
forfiles /p "C:\path\to\source" /m *.pdf /c "cmd /c copy @path C:\path\to\destination"
```
{% endcode %}

Print the names of all txt files in a directory

```powershell
forfiles /p "C:\path\to\directory" /m *.txt /c "cmd /c echo @file"
```

Rename all .docx files in the current directory to start with "Document\_":

```powershell
forfiles /s /m *.docx /c "cmd /c ren @file Document_@file"
```

Change the extension of all .txt files to .bak in a directory

```powershell
forfiles /p "C:\path\to\directory" /m *.txt /c "cmd /c ren @file @fname.bak"
```

Recursively list the paths of all files in a directory and its subdirectories

```powershell
forfiles /p "C:\path\to\directory" /s /c "cmd /c echo @path"
```

Log the names and sizes of all .exe files in the current directory and subdirectories:

```powershell
forfiles /s /m *.exe /c "cmd /c echo @file (@fsize)" >> exe_files.log"
```

Execute a PowerShell command on each file in a directory

{% code overflow="wrap" %}
```powershell
forfiles /p "C:\path\to\directory" /m *.* /c "cmd /c powershell -Command \"Some-PowerShell-Command -Argument @file\""
```
{% endcode %}

Print the last modified date of all files in a directory

```powershell
forfiles /p "C:\path\to\directory" /c "cmd /c echo @file @fdate"
```

Create a directory for each file in a directory (using the file name as the directory name)

```powershell
forfiles /p "C:\path\to\directory" /m *.* /c "cmd /c mkdir @fname"
```

<mark style="color:yellow;">`@file`</mark>

Represents the full path of the current file being processed by the loop or command.

Its value changes as the loop iterates through a set of files.

Use it within commands to perform actions specific to each file, like copying, deleting, or hashing.

<mark style="color:yellow;">`@date`</mark>

Holds the date and time associated with the current file being processed.

The specific format of @date depends on the command being used.

forfiles typically provides access to date components like creation, modification, or access time.

It allows comparing file dates with specific criteria within the loop.
