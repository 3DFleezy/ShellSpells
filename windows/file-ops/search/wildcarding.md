# Wildcarding

`*`= stands for zero or more characters

`?` = any single character

In my testing, it appears that '?' does not work in place of '.'

Example:

A folder contains many files, one is called 'example.txt'

If I use <mark style="color:yellow;">`Get-ChildItem -Name ???????????`</mark>

It does not find the file.

If I use <mark style="color:yellow;">`Get-ChildItem -Name ???????.???`</mark>

It will find the file.
