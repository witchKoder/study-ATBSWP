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
Example:
Path.cwd().is_absolute() returns True.
Path('comics\\villians\\catwoman').is_absolute() returns False
To turn a relevant path into a absolute path, put the Path.cwd() function before the path object. Similarly, the absolute() method shortens the process and returns the absolute path of a relevant path.
The Path.home() will accomplish the same as Path.cwd().

# Creating new folders
Your programs can create folders by using the os module and calling the makedirs() function.
Example:
os.makedirs('C:\\USERS\Nicky\\comics//villians//catwoman')
Note that this will create the necessary folders in order to reach the catwoman directory.

To make a folder from an existing path object, call the mkdir() method on such object. This method is unable to make any necessary folders leading up to it, so make sure the folders exist before hand. However, you can force the mkdir method to make parent folders by passing the argument, parents=True. This will create all necessary folderes to reach the last folder specified.

# Getting parts of the file path
Given a path object, you can use attributes to return string values of the various parts of the path. This is especially useful if you are creating new file paths with already existing folders.
The parts of a file path include:
* The Anchor
The root folder 'C:\\'
* The Drive
The single letter that represents the physical hardrive/ storage. 'C:'
* The Parent
The parent attribute is the folder containing the file
* the Stem
The stem is the name of the file
* The suffix
The suffix is the extension of the fileMost of the attributes return string values, except for the parent attribute. The parent attribute returns another path object. You can also return a tuple containing all the different string values using the parts attribute.

Furthermore, there is another attribute called parents. The parents attribute will return a path object's ancestor folders by passing in an  index.
Example:
path = WindowsPath('C:\\USERS\\Nicky\\Music\\Projects')
path.parents[0] returns WindowsPath('C:\\USERS\Shann\\Music')
path.parents[1] returns WindowsPath('C:\USERS\\Nicky')

## Finding File Sizes and Time Stamps
The stat() method returns a stat_result object containing file size and time stamp information about a file.
there several important attributes to the stat_result.
* st_size
This is returned as bytes, so to convert it to kb, mb, or gb, do some sort of division by 1024. path.stat().st_size / 1024 ** 2 returns gb
* st_mtime
returns the last modified date, and requires time module to humanly read it.
* st_ctime
provides the date at which the file was created, and requires time module to humanly read it. time.asctime(time.localtime(path.stat().st_ctime))

## Finding Files Using Glob Patterns
Glob patterns are essentially a simplified regex language. In fact, the asterisk and question mark achieve the exact same goal in normal regex. That is, the asterisk is greedy, and the question mark is not greedy.
The characters
1. * (asterisk)
Copies all characters
2. ? (question mark)
Copies only one character
can be used to match both folders and files in glob patterns.
Path objects that are folders has a glob() method. Once the glob method is called, the method will provide a listing of elements that follow the glob pattern's argument - returning a generator object. You can pass the generator object to the list constructor.
Example:
Assume that my_path lies in the video folder,
my_path.glob('*') will return every file as a generator object
You can call list or a for loop to extract the contents,
for name in Path()'C:\\USERS\\Shann\\Music'):

Some use cases, for instance, include renaming or backing up folders and files. Also, the glob patterns are most commonly used with the cli with commands like ls and dir.

# Checking the Validity of a Path
In order to not recieve an error because a folder or file does not exist, you must call the build-in method exists() on the path object. The exists() method returns True or False 
You can check if the file exists with the is_file() method checks if the path object is a true file.
Calling is_dir() method on a path object checks if the path object is a true folder.

# The Reading and Writing Process
In this next section, the functions covered only handle plain text extensions. A plain text file only includes plain text, and do not include font, size, or color. For instance, .txt and .py are considered plain text extensions. Essentially, you can open up the file in a text editor and the program can read the file and treat it as a string value.

All other files are binary type. This includes img, docx, pdfs, spreadsheets and executables.
Upon opening the file in the text editor, a random sequence of scrambled characters will appear. Unfortunately, all binary files must be approached differently. Although modules stream line this process for us. One such being the shelve module.

An uncommon way of reading and writing to files is to use the pathlib's methods, read_text() method and write_text() method.
The read_text() method rreturns the contents of the path object's file to a string value.
The write_text() method on a path object's file creates or over writes an existing file with the string passed into it.
Note that this uncommon way to read and write to a file is limited to basic interactions with the files and folders.

The more common way is to use the open function. There are three steps to the model of writing/reading to a file.
1. Call the open() function to return a file object
2. Call the read() or write() method on the file object.
3. Call the close() method on the file object. 

## Opening Files
Call the open() function and pass an argument that is the desired path. It can be either an absolute path or a relevant path. The return value is a file object.
Example:
default_open_file = Path(f'{Path.home()} \/ Documents \/ catwoman.txt', encoding='UTF-8') # opens catwoman.txt in utf-8
In this default open function, the file is in reading plaintext mode. You are unable to write and only allowed to read. Hence the name.

You can pass the file path, mode to interact with the file, and the encoding, as arguments  to the open function
The three modes are read ('r'), write ('w') and append ('a'). It is best to always assign utf 8 to encoding.

## Reading Files
Since we have the file object default_open_file, we can now read from the source by calling the read() method on the file object.
Example:
default_open_file.read() # returns any text in the file object as a large string value.

Another and easier way to read files is the readlines() method. The long string value returned will now appear as a list. At which point, the string value will become multiple elements in the list if and only if there is a line break. The program automatically adds escape characters to each end of string value, unless the string value is the last element within the data structure.

## Writing to files
In order to write to files, be sure that the file object has the writing argument passed into the open function. In fact, you can also decide to choose append mode instead of writing mode.
The writing mode overwrites a file. Meanwhile, the append mode continues to write to an existing file or creates a new file if the file does not already exist.
Example:
open_file = Open()'C:\\USERS\\Shann\\Documents\\catwoman.txt', 'a')
open_file.write('Purr')
open_file.close()

read_file = open('C:\\USERS\\Shann\\Documents\\catwoman.txt', 'r', encoding='utf-8')
read_file_contents = read_open_file.read()
.read_open_file.close()
print(read_file_contents)
Note that the append mode does not add an escape character newline upon writing to file and closing the file. You must pass the character in your .write() method string.

# Using with statements
Every file that is open needs a close method called to the file object in order to close the file. The with statement is a pythonic way to write open and close on a file object.
The with creates a context manager that manages Python's resources. Some of the resources are files, network connections, or segments of of memory. Most of the time, the resources have setup and teardown steps of which the resource is allocated and released so other programs can use it.

The with statement forms a block of code that begins to allocate the resources, which until the closing of the with statement. The closing of the with statement can appear as a return statement, a file handling error, or an other reason. This is is where resources are released.
Example:
with open('C:\\USERS\\Nicky\\Documents\\catwoman.txt', 'w', encoding='UTF-8') as file_object:

# closes once the block is exited.

# Saving variables with the shelve module
To be able to save variables for the next time you run the script, you can use the shelve module. The variables are stored in binary shelve files. You can add save and open features to a program, for example, config settings. Once the file is loaded up again, the config settings will be restored.
Example:
import shelve
shelve_file_object = shelve.open('C:\\USERS\\Nicky\\Documents\\comics')
shelve_file_object['villians'] = ['catwoman', 'poison ivy']
shelve_file_object.close()
Notice that the shelve file opens and closes exactly like opening and writing files without the shelve module. Pass a path into the argument, though we initialize a list with villians. The shelve treats the variables as a key to a dictionary. Once the code block is executed, three files are created: comics.bak, comics.dat, and comics.dir

Unlike normal open to close reading to writing, the shelve module does not need specifying what mode it should be in, as it allows for reading and writing once opened.
Example:
shelve_file_object = open('C:\\USERS\\Nicky\\Music\\comics')
shelve_file_object['villians'] # returns the values of the list
shelve_file_object.close()
We use the shelve_file_object['villians'] as a key to find the values, because the shelve_file_object returns a dictionary variable.
to extract the keys and values, you must pass tthe list constructor.
Example:
shelve_file_object  open()'C:\\USERS\\Nicky\\Music\\comics')
list(shelve_file_object.keys()) # returns []'comics']
list(shelve_file_object.values()) # returns ['catwoman'', 'poison ivy']
shelve_file_object.close()

