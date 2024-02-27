# Size

| Command                                                                                                     | Description                                         |
| ----------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| <mark style="color:yellow;">`dir /O /S`</mark>                                                              | Sort by size, recursive                             |
| <mark style="color:yellow;">`forfiles /M *.docx /C "cmd /c echo @fsize @path"`</mark>                       | Show size by file extension                         |
| <mark style="color:yellow;">`dir /W /O /S \| findstr ">100000"`</mark>                                      | Greater than 100KB, recursive                       |
| <mark style="color:yellow;">`forfiles /S /C "cmd /c if @fsize gtr 55 echo @path"`</mark>                    | Greater than 55 bytes, recursive                    |
| <mark style="color:yellow;">`forfiles /S /M *.* /Q >1048576`</mark>                                         | Greater than 1 MB, recursive                        |
| <mark style="color:yellow;">`Get-ChildItem "C:\path" -Recurse \| Where-Object { $\_.Length -gt 55 }`</mark> | Greater than 55 bytes (size in bytes), recursive    |
| <mark style="color:yellow;">`dir /W /O /S \| FINDSTR "<100000"`</mark>                                      | Less than 100KB, recursive                          |
| <mark style="color:yellow;">`forfiles /S /C "cmd /c if @fsize ! gtr 55 echo @path"`</mark>                  | Less than 55 bytes, recursive (Not > 55), recursive |
| <mark style="color:yellow;">`forfiles /S /M *.* /Q >1048576`</mark>                                         | Less than 1 MB, recursive                           |
| <mark style="color:yellow;">`Get-ChildItem "C:\path" -Recurse \| Where-Object { $\_.Length -lt 55 }`</mark> | Less than 55 bytes (size in bytes), recursive       |
