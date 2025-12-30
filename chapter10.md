# Chapter 10 - Reading & Writing Files
There are two main components to a file
1. A filename
written as one word, or words lacking spaces.
2. A Path
Describes where the file resides on the computer.
The final period is called the file's extension, such as .md.
The beginning of the path that starts with C:\ is called the root path. This is where most folders lie. Other root paths contain dvd drives and usb flash drives.
## Standardizing Path Separators
Windows operating systems use backslashes to separate paths. Meanwhile, other operating systems do not. Therefore when using the Path function of the pathlib module, use forward slashes as the module will automatically translate the symbol to the correct style  to the operating system.
Example:
from pathlib import Path
Path('comics', 'villians', 'catwoman')
WindowsPath('comics/villains/catwoman')
str(Path('comics', 'villians', 'poisonivy'))
'comics//villians//poisonivy'
Notice that once you call the str function on the Path function, the value contains the proper operating systems path separators.

## Joining Paths
Similar to the plus concatenation operator + that is used on strings types and int types, paths use the divide symbol to concatenate.
This is especially handy if you had already declared the Path object and wanted to add to it.
Example:
Path('dramas') / 'english' / 'shakespear'
WindowsPath('dramas/english/shakespear')
Path('dramas') / Path('english/shakespear')
WindowsPath('dramas/english/shakespear')
Path('dramas') / Path('english') / Path('shakespear')
WindowsPath('dramas/english/shakespear')
When executing Path functions, keep in mind that it reads from left to right and needs at least one of the first two values to be a Path object. The forward dash can used on another path object or a single string, NOT two string values. Otherwise, a TypeError will be raised.

