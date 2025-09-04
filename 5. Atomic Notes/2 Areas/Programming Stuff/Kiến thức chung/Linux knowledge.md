2025-08-30 10:03
Status: #baby
Tags: [[os]]
## Main

## Kill process on ports: 
To list any process listening to the port 8080:
```
lsof -i:8080
```
To kill any process listening to the port 8080:
```
kill -9 $(lsof -t -i:8080)
```

## Rename a file
`mv old_file_path new_file_path`

## Know path of a variable
`which ...` 
eg: `which java/python`
> /usr/bin/java(python)

## Read link
`readlink:` whenever we have a symbolic link and we want to know what path it represents. Then, in that case, the _readlink_ command comes into play to show the actual path of the symbolic link

![](https://media.geeksforgeeks.org/wp-content/uploads/20190404032504/Screenshot-from-2019-04-04-03-24-48.png)

`readlink -f:` This option canonicalize by following every symlink in every component of the given name recursively; all but the last component must exist

## Export 
**export** is bash shell BUILTINS commands, which means it is part of the shell. It marks an [environment variables](https://www.geeksforgeeks.org/environment-variables-in-linux-unix/) to be exported to child-processes.
```export [-f] [-n] [name[=value] ...] or export -p```
- **Without any argument :** To view all the exported variables.
- **-p :** To view all exported variables on current shell.
- **-f:** It must be used if the names refer to functions. If -f is not used, the export will assume the names are variables
![Lightbox](https://media.geeksforgeeks.org/wp-content/uploads/export_3.png)
- **name[=value]:** You can assign value before exporting using the following syntax
![export_4](https://media.geeksforgeeks.org/wp-content/uploads/export_setting_var.png)
- **-n:** Named variables (or functions, with -f) will no longer be exported.
In general, the export command marks an environment variable to be exported with any newly forked child processes and thus it allows a child process to inherit all marked variables

## See all hidden file: 
`ls -a`: show just file name
`ls -la`: show owner and file name

## jps: 
jps - list the instrumented JVMs on the target system

## Fix the problem of read-only file in NTFS
`sudo apt-get purge ntfsprogs -y`
`sudo apt-get ntfs-3g -y`
`sudo apt-get install ntfs-3g -y`
Then choose your partitions to fix the problem
`sudo ntfsfix /dev/sdb123....`

## Run .run file: 
1.  Open the Ubuntu terminal and move to the folder in which you've saved your RUN file.
2.  Use the command **chmod +x yourfilename.run** to make your RUN file executable.
3.  Use the command **./yourfilename.run** to execute your RUN file.


## Bashrc 
**.bashrc**: A bashrc file is a shell script file that Linux uses when starting up to load items like modules and aliases into your profile. Your bashrc file lives in your /home directory. You can make changes to it with a text editor like [nano](https://www.nano-editor.org/). Adding sections to your bashrc file, such as adding modules to load when you sign in or assigning aliases for commands that you use frequently, can be time savers for your workflows.
### Defining functions in bashrc
```bash
today()
{
 echo` ``This is a ` ```date` `+``"%A %d in %B of %Y (%r)"``` ` `` `return`
}
```
To reflect the changes in the bash, either exit and launch the terminal again 
Or use the command:
```bash
$source .bashrc
```
To run the function just created call today :
```bash
$ today
```
Result: 
![Today](https://www.journaldev.com/wp-content/uploads/2020/06/today.png)

```bash
mkcd () 
{
	mkdir -p --"$1" && cd -P -- "$1"
}
```
Add alias: 
`alias wmi='whoami'`

## Create xampp short cut 
Recently, I try to install Xampp on Ubuntu, after installing successfully, I recognized that Xampp is not showed up on Ubuntu start menu automatically, then I worked around and found out the solution to create Xampp shortcut on Start Menu.

1.  Firstly, `cd` to`/usr/share/applications` then create a new file with extension is `*.desktop` by opening the terminal then run this command: `sudo touch xampp.desktop`.
2.  Open the new file with super admin right by: `sudo gedit xampp.desktop`
3.  Paste following to the file content:

```txt
[Desktop Entry]
Encoding=UTF-8
Name=XAMPP Control Panel
Comment=Start and Stop XAMPP
Exec=sudo /opt/lampp/manager-linux-x64.run
Icon=/opt/lampp/htdocs/favicon.ico
Categories=Application
Type=Application
Terminal=true
```

`Exec`: Command to run the application (with Xampp you need `sudo` right).  
`Terminal`: `true` if you want to open terminal when running this application. With Xampp I set value is `true` to type the password of `sudo` when running the app.

4.  Save the file, now you have the Xampp shortcut available on start menu. Hit Windows button to check it :).

## Fix read-only file ntfs: 
`sudo fdisk -l` to see all partitions in4
`sudo ntfsfix path_to_partitions` to fix read-only problem

## References
