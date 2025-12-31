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

# Accessing Working Directory
All programs have a working directory. Those who do not appear to contain the root directory, is to assume it's located in the current working directory.
You can receive the string value of the current working directory by using Path.cwd() function.
You can change working directories by using the os.chdir() function
Notice pathlib and os modules are now being deployed, because pathlib is unable to change directories.

## Accessing the home directory
All users have their unique user folders that contain all their files. This unique folder is called the home directory, and appears as C:\USERS\name
To quickly obtain the home directory, use the Path.home() to access the home directory.


# Specifying Absolute & Relevant Paths
There are two ways to specify a path
1. Absolute path
An absolute path always consists of the root directory
2. relevant path
a relevant path refers to the current working directory for a program
history: In 1960s, computers had two floppy discs labeled A and B. On windows, dbd and usbs are labeled d or higher.

## Handling Absolute & Relevant Paths
Calling the is_absolute()) method on a path object will return True, if the path object reflects an absolute path. Otherwise, the evaluation will return False.


