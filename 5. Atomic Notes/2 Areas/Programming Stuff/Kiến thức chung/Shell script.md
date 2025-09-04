2025-08-30 09:55
Status: #baby
Tags: [[productivity]]
## Main


gitl## Shell Prompt
	The prompt, **$**, which is called the **command prompt**, is issued by the shell. While the prompt is displayed, you can type a command
## Shell Types
-   **Bourne shell** − If you are using a Bourne-type shell, the **$** character is the default prompt.
	-   Bourne shell (sh)
	-   Korn shell (ksh)
	-   Bourne Again shell (bash)
	-   POSIX shell (sh)
	
	Bourne shell is usually installed as **/bin/sh** on most versions of Unix. For this reason, it is the shell of choice for writing scripts that can be used on different versions of Unix. We are going to cover most of the Shell concepts that are based on the Borne Shell.
    
-   **C shell** − If you are using a C-type shell, the % character is the default prompt.
	-   C shell (csh)
	-   TENEX/TOPS C shell (tcsh)	

## Shell Scripts
The basic concept of a shell script is a list of commands, which are listed in the order of execution. A good shell script will have comments, preceded by **#** sign, describing the steps

Shell scripts and functions are both interpreted. This means they are not compiled

### Example
Note all the scripts would have the **.sh** extension
Before you add anything else to your script, you need to alert the system that a shell script is being started. This is done using the **shebang** construct
> #!/bin/sh

This tells the system that the commands that follow are to be executed by the Bourne shell

Need to make the script executable: 
```
$chmod +x test.sh
```

## Variable names
The name of a variable can contain only letters (a to z or A to Z), numbers ( 0 to 9) or the underscore character ( _).

By convention, Unix shell variables will have their names in UPPERCASE

Valid: 
_ALI
TOKEN_A
VAR_1
VAR_2

Invalid:
2_VAR
-VARIABLE
VAR1-VAR2
VAR_A!

### Define
variable_name=variable_value
> NAME="Zara Ali"

### Accessing Values
To access the value stored in a variable, prefix its name with the dollar sign (**$**)
> echo $NAME

### Read-only Variables
> NAME="Zara Ali" 
> readonly NAME
   NAME="Qadiri"
   
  => Wrong
 
 ### Unsetting Variables
 Unsetting or deleting a variable directs the shell to remove the variable from the list of variables that it tracks. Once you unset a variable, you cannot access the stored value in the variable
> NAME="Zara Ali"
>  unset NAME
>  echo $NAME

The above example does not print anything. You cannot use the unset command to **unset** variables that are marked **readonly**

### Variable Types
-   **Local Variables** − A local variable is a variable that is present within the current instance of the shell. It is not available to programs that are started by the shell. They are set at the command prompt.
    
-   **Environment Variables** − An environment variable is available to any child process of the shell. Some programs need environment variables in order to function correctly. Usually, a shell script defines only those environment variables that are needed by the programs that it runs.
    
-   **Shell Variables** − A shell variable is a special variable that is set by the shell and is required by the shell in order to function correctly. Some of these variables are environment variables whereas others are local variables.

## Special var
| Sr.No. | Variable and Description |
| -------  | ------------ |
| 1 | **$0** The filename of the current script.|
| 2| **$n** These variables correspond to the arguments with whicha script was invoked. Here **n** is a positive decimal number corresponding to the position of an argument (the first argument is $1, the second argument is $2, and so on)|
| 3 |**$#**  The number of arguments supplied to a script. |
|4 |**$** All the arguments are double quoted. If a script receives two arguments, $* is equivalent to $1 $2.|
| 5 |**$@** All the arguments are individually double quoted. If a script receives two arguments, $@ is equivalent to $1 $2.|
| 6 |**$?** The exit status of the last command executed. |
| 7 |**$(2 cái)** The process number of the current shell. For shell scripts, this is the process ID under which they are executing.| 
| 8 | **$!** The process number of the last background command.|

#### Exit status
The **$?** variable represents the exit status of the previous command.

Exit status is a numerical value returned by every command upon its completion. As a rule, most commands return an exit status of 0 if they were successful, and 1 if they were unsuccessful.
Some commands return additional exit statuses for particular reasons. For example, some commands differentiate between kinds of errors and will return various exit values depending on the specific type of failure.

## Shell arrays
A shell variable is capable enough to hold a single value. These variables are called scalar variables
Shell supports a different type of variable called an **array variable**. This can hold multiple values at the same time. Arrays provide a method of grouping a set of variables. Instead of creating a new name for each variable that is required, you can use a single array variable that stores all the other variables.

### Defining Array Values
*simple creating: *

```
array_name[index]=value
```
> NAME[0]="Zara" NAME[1]="Qadir" NAME[2]="Mahnaz" NAME[3]="Ayan" NAME[4]="Daisy"

*array initialization: *
```
array_name=(value1 ... valuen)
```

*access: *
```
${array_name[index]}
```

> NAME[0]="Zara" NAME[1]="Qadir" NAME[2]="Mahnaz" NAME[3]="Ayan" NAME[4]="Daisy" echo "First Index: ${NAME[0]}" echo "Second Index: ${NAME[1]}"

*access all the items:*
```
${array_name[*]}
${array_name[@]}
```

## Basic Operators
The following points need to be considered while adding −

-   There must be spaces between operators and expressions. For example, 2+2 is not correct; it should be written as 2 + 2.
    
-   The complete expression should be enclosed between **‘ ‘**, called the backtick

### Arithmetic Operators	
> ``` + -  * / % = == !=  as usual```
It is very important to understand that all the conditional expressions should be inside square braces with spaces around them, for example **[ $a == $b ]** is correct whereas, **[$a==$b]** is incorrect
All the arithmetical calculations are done using long integers.
### Relational Operators
**a** holds 10 and variable **b** holds 20

- **-eq**
Checks if the value of two operands are equal or not; if yes, then the condition becomes true. [ $a -ne $b ] is true.
- **-ne**
Checks if the value of two operands are equal or not; if values are not equal, then the condition becomes true. [ $a -eq $b ] is not true.
- **-gt**

Checks if the value of left operand is greater than the value of right operand; if yes, then the condition becomes true.
- **-lt**

Checks if the value of left operand is less than the value of right operand; if yes, then the condition becomes true.
- **-ge**

Checks if the value of left operand is greater than or equal to the value of right operand; if yes, then the condition becomes true.
- **-le**

Checks if the value of left operand is less than or equal to the value of right operand; if yes, then the condition becomes true.

###  Boolean Operators
- **!**

This is logical negation. This inverts a true condition into false and vice versa.
- **-o**

This is logical **OR**. If one of the operands is true, then the condition becomes true.
- **-a**

This is logical **AND**. If both the operands are true, then the condition becomes true otherwise false.

###  String Operators
**a** holds "abc" and variable **b** holds "efg" then
- **=**

Checks if the value of two operands are equal or not; if yes, then the condition becomes true.
- **!=**

Checks if the value of two operands are equal or not; if values are not equal then the condition becomes true.
- **-z**

Checks if the given string operand size is zero; if it is zero length, then it returns true.
- **-n**

Checks if the given string operand size is non-zero; if it is nonzero length, then it returns true.
- **str**

Checks if **str** is not the empty string; if it is empty, then it returns false.
[ $a ] is not false.
### File Test Operators
Tự tìm hiểu
## Shell Decision Making
### The if...else statements
-   [if...fi statement](https://www.tutorialspoint.com/unix/if-fi-statement.htm)
-   [if...else...fi statement](https://www.tutorialspoint.com/unix/if-else-statement.htm)
-   [if...elif...else...fi statement](https://www.tutorialspoint.com/unix/if-elif-statement.htm)

### The case...esac Statement
Unix Shell supports **case...esac** statement which handles exactly this situation, and it does so more efficiently than repeated **if...elif** statements
-   [case...esac statement](https://www.tutorialspoint.com/unix/case-esac-statement.htm)
## Shell Loop Types
### Nesting while Loops
```
while command1 ; # this is loop1, the outer loop
do
   Statement(s) to be executed if command1 is true

   while command2 ; # this is loop2, the inner loop
   do
      Statement(s) to be executed if command2 is true
   done

   Statement(s) to be executed if command1 is true
done
```

## Substitution
The shell performs substitution when it encounters an expression that contains one or more special characters.

| Sr.No. | Escape & Description |
| -- | -- |
| 1	| `\\` backslash |
| 2 | **\a** alert (BEL)|
| 3 |**\b** backspace
| 4|**\c** suppress trailing newline
|5|**\f** form feed
|6|**\n** new line
|7|**\r** carriage return
|8|**\t** horizontal tab
|9|**\v** vertical tab

You can use the **-E** option to disable the interpretation of the backslash escapes (default).

You can use the **-n** option to disable the insertion of a new line.

### Command Substitution
Command substitution is the mechanism by which the shell performs a given set of commands and then substitutes their output in the place of the commands
The command substitution is performed when a command is given as
`command`
```
#!/bin/sh DATE=`date` echo "Date is $DATE" USERS=`who | wc -l` echo "Logged in user are $USERS" UP=`date ; uptime` echo "Uptime is $UP"
```

###  Variable Substitution
Sr.No.| Form & Description
-- | -- 
1 | **${var}** Substitute the value of _var_.
2 |**${var:-word}** If _var_ is null or unset, _word_ is substituted for **var**. The value of _var_ does not change.
3 | **${var:=word}** If _var_ is null or unset, _var_ is set to the value of **word**.
4 |**${var:?message}** If _var_ is null or unset, _message_ is printed to standard error. This checks that variables are set correctly
5 |**${var:?message}** If _var_ is set, _word_ is substituted for var. The value of _var_ does not change.

##  Shell Quoting Mechanisms
### The Metacharacters
```* ? [ ] ' " \ $ ; & ( ) | ^ < > new-line space tab```

Sr.No | Quoting & Description
-- | -- 
1 | **Single quote** All special characters between these quotes lose their special meaning.
2 | **Double quote** Most special characters between these quotes lose their special meaning with these exceptions: $, \`, \$, \\', \\", \\\
3 | **Backslash** Any character immediately following the backslash loses its special meaning.
4 | **Back quote** Anything in between back quotes would be treated as a command and would be executed.

## IO Redirections
### Output Redirection
The output from a command normally intended for standard output can be easily diverted to a file instead. This capability is known as output redirection.

If the notation > file is appended to any command that normally writes its output to standard output, the output of that command will be written to file instead of your terminal.

Check the following **who** command which redirects the complete output of the command in the users file.

> $ who > users

Notice that no output appears at the terminal. This is because the output has been redirected from the default standard output device (the terminal) into the specified file. You can check the users file for the complete content

``` 
$ cat users
oko         tty01   Sep 12 07:30
ai          tty15   Sep 12 13:32
ruth        tty21   Sep 12 10:10
pat         tty24   Sep 12 13:07
steve       tty25   Sep 12 13:03
$
```
You can use >> operator to append the output in an existing file as follows
`$ echo line 2 >> users`

### Input Redirection
Just as the output of a command can be redirected to a file, so can the input of a command be redirected from a file. As the **greater-than character >** is used for output redirection, the **less-than character <** is used to redirect the input of a command.
https://www.tutorialspoint.com/unix/unix-io-redirections.htm

### Here Document
A **here document** is used to redirect input into an interactive shell script or program.

We can run an interactive program within a shell script without user action by supplying the required input for the interactive program, or interactive shell script.

The general form for a **here** document is

### Discard the output
Sometimes you will need to execute a command, but you don't want the output displayed on the screen. In such cases, you can discard the output by redirecting it to the file **/dev/null** −
> $ command > /dev/null

Here command is the name of the command you want to execute. The file **/dev/null** is a special file that automatically discards all its input.

To discard both output of a command and its error output, use standard redirection to redirect **STDERR** to **STDOUT**

> command > /dev/null 2>&1

Here **2** represents **STDERR** and **1** represents **STDOUT**. You can display a message on to STDERR by redirecting STDOUT into STDERR as follows
> $ echo message 1>&2

### Redirection Commands
No | Command
-- | -- 
1 | **pgm > file** Output of pgm is redirected to file
2 | **pgm < file** Program pgm reads its input from file
3 | **pgm >> file** Output of pgm is appended to file
4 | **n > file** Output from stream with descriptor **n** redirected to file
5 | **n >> file** Output from stream with descriptor **n** appended to file
6 | **n >& m** Merges output from stream **n** with stream **m**
7 | **n <& m** Merges input from stream **n** with stream **m**
8 | **<< tag** Standard input comes from here through next tag at the start of line
9 | **\|** Takes output from one program, or process, and sends it to another

Note that the file descriptor **0** is normally standard input (STDIN), **1** is standard output (STDOUT), and **2** is standard error output (STDERR).


## References
