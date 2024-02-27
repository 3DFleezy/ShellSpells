# Insert

## Strings

Workaround to insert text (`New Text`) <mark style="color:orange;">before</mark> or <mark style="color:orange;">after</mark> a specific pattern (`Some Text`) by recreating the file.

This example doesn't directly insert but rebuilds the file with additional text (NEED TO TEST)

{% code overflow="wrap" %}
```powershell
type file.txt | find /v "Some Text" > temp.txt && echo New Text >> temp.txt && type temp.txt > file.txt
```
{% endcode %}

Insert <mark style="color:orange;">Before</mark> a specific pattern.

Adjust the `-replace` pattern to change where the text is inserted:

{% code overflow="wrap" %}
```powershell
$content = Get-Content file.txt; $newContent = $content -replace "Pattern", "New Text$0"; $newContent | Set-Content file.txt
```
{% endcode %}

Insert <mark style="color:orange;">Before</mark> a Specific Pattern:

This script inserts "Your new text here" before the first occurrence of "specific pattern" in file.txt:

{% code overflow="wrap" %}
```powershell
$content = Get-Content -Path file.txt
$index = $content | Select-String -Pattern "specific pattern" -SimpleMatch | Select-Object -First 1 -ExpandProperty LineNumber
$before = $content[0..($index-2)]  # Lines before the pattern
$after = $content[($index-1)..($content.Length-1)]  # Lines including and after the pattern
$newContent = $before + "Your new text here" + $after
$newContent | Set-Content -Path file.txt
```
{% endcode %}

Similar to the above, this command inserts "New Text" by replacing a specific pattern ("Pattern") in the file:

```powershell
(Get-Content file.txt) -replace 'Pattern', 'New Text' | Set-Content file.txt
```

Insert <mark style="color:orange;">After</mark> a specific pattern:

```powershell
findstr /s /i "<pattern>" <filename> > temp.txt
echo "<string/line>" >> temp.txt
move temp.txt <filename>
```

## Lines

Add line numbers:

```powershell
type C:\file.txt | find /n /v ""
```

Displays each line of a file with line numbers:

```powershell
findstr /n "^" C:\file.txt
```

Add line numbers to the content of a file:

{% code overflow="wrap" %}
```powershell
Get-Content C:\path\to\file.txt | ForEach-Object { $i++; "$i $_" } | Set-Content C:\path\to\numberedfile.txt
```
{% endcode %}

Inserting Text at the Beginning of a File:

```powershell
$text = "Your new text here`n" + (Get-Content file.txt -Raw)
Set-Content -Path file.txt -Value $text
```

Inserting Text After a Specific Line: Adjust <mark style="color:yellow;">`[0..($content.Count-1)]`</mark> to target a different line.

{% code overflow="wrap" %}
```powershell
$content = Get-Content -Path file.txt
$modifiedContent = $content[0..($content.Count-1)] + "Your new text here" + $content[$content.Count..($content.Count)]
Set-Content -Path file.txt -Value $modifiedContent
```
{% endcode %}

Add line at specific point (NEED TO TEST):

{% code overflow="wrap" %}
```powershell
@echo off
for /f "delims=" %%a in (<filename>) do (
  if %%a==<pattern> (
    echo "<string/line>"
  )
  echo %%a
) > temp.txt
move temp.txt <filename>
```
{% endcode %}
