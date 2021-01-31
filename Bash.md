- [Bash](#bash)
  - [Bash Vs Terminal](#bash-vs-terminal)
  - [Terminal Commands vs Bash Scripting](#terminal-commands-vs-bash-scripting)
  - [Terminal Commands](#terminal-commands)
  - [Bash Scripting](#bash-scripting)
    - [Shebang](#shebang)
      - [Comments](#comments)
    - [Variables](#variables)
      - [User Input](#user-input)
      - [Comparision operators](#comparision-operators)
    - [Command Substitution](#command-substitution)
    - [Redirection](#redirection)
    - [Arithmetic operations](#arithmetic-operations)
    - [Relative vs Absolute path.](#relative-vs-absolute-path)
    - [Functions](#functions)
    - [Arrays](#arrays)
    - [Regex](#regex)
    - [SED](#sed)
    - [Shell Flow Control](#shell-flow-control)
      - [If](#if)
        - [Test](#test)
      - [Select](#select)
        - [case](#case)
        - [break](#break)
        - [continue](#continue)
      - [For loop](#for-loop)
      - [While loop](#while-loop)
      - [Until loop](#until-loop)
    - [Signal](#signal)
    - [Trap](#trap)
    - [Extras](#extras)








# Bash
**Kernel** is the code that interacts with bios/hardware.Most important part of a pc.       
But having access to kernel directly is not very good mostly dangerous.So a abstraction layer is built on top of kernel called Shell.      
* A shell can be written in any programming language,that gives input to kernel.We access shell through a terminal emulator.There are various shells, and emulators.
* The shell(sh) was the first shell created and used by programmers,after that came ksh,csh for different small(niche) groups of developers.
* Bash was invented in 1989,(Bourne Again shell),it was backwards compatible with other systems,and POSIX standards compliant.So many programmers used this,and some even improved on top of it.
* Now bash is every where with combination of a linux kernel.
* It is the default shell in most/all distro's of **GNU/linux** and Mac OS X.(unix based)
* Some of the new bash forks that are in rise are zsh(z shell) designed in 2000's and is backwards compatible with bash.Some more shells are fish(friendly interactive shell),Dash(Debian Almquist Shell)
* Most scripts and tools around the internet are created using Bash.

## Bash Vs Terminal
* Bash is a shell and terminal is a ui to access the shell.
* Bash is a Command Line Interface,works by taking commands from user(terminal).
* While terminal *accesses* shell,it is *not* a shell,it takes user input from keyboard and passes it to shell,and displays the output in it,This is a CLI.
* There are many terminals,of which popular are Konsole(kde default),g-terminal(gnome default),x-terminal(xfce default),guake(gnome drop down terminal),yakuake(kde drop down terminal),terminator,termux,tilus,etc,.
* When we open a terminal emulator we are greated with the default shell(Bash mostly) of the pc
* The data we pass with a command is called command line arguments.

## Terminal Commands vs Bash Scripting
While there are thousands of terminal commands, there are only few bash scripting commands/options.     
This is because we use the terminal commands in a predefined structure to make them perform what we desire using a bash script.        
Bash offers mostly a structure and general rules of using group of terminal commands, for a specific task.
> Ex:cd is a terminal(bash) command to change directory
>while a file.sh is used to perform tasks that can use the cd command.

## Terminal Commands
[Terminal Commands](./Administration.md#linux-commands) 
## Bash Scripting
A Bash script is a file with all terminal commands in order of operation.This has a extension **.sh/.bash**.
* we can use any one of multiple shells for scripting but most common and wide spread is Bash.

### Shebang
`#!/bin/bash`      
This is used to tell the interpreter which shell to use(if multiple shells are present in the user's operating system).
#### Comments
`#` sign is used to comment out code in script.       
To run a script file we need to have appropriate permissions for it.To change permission use **chmod**.

>chmod +x file.sh     

We can run the file in multiple ways.They are,        
* bash file.sh        
* ./file.sh(only works on native drive, may not work in mounted drives)(when the terminal is opened in that directory)
* sh ./file.sh
* all statements can end with **;** but it is a preferrence rather than need in most cases.

### Variables
In Bash,variables are used to store a value,file location,script name,just about anything we may use repeatedly in the script.
>variable_name="value"          
>echo $variable          
>variable=$(date) gives the value of date as a variable          
* To access a variable we use a $ sign infront of variable differentiates it from a terminal command.
* To take the output of a command and store it in a variable we use $(command)
* ${variable} is used to concatenate values
* No spaces before and after '=' in bash
* Prefer allcaps for variables.use good naming conventions that are consistent
> Ex: date is a terminal command, we can have a date variable but accessed by $date.      

#### User Input
Taking user input is crucial to many programs we do this many ways.       
Easy and most preferred is using *read*     

**read**: takes the input from keyboard/standard input and stores in a variable.if no variable name is given stores in default *REPLY* variable
* *-p* Can prompt user/display text on screen for asking what he needs to input,only one line prompts are possible
* *-s* Won't show any thing on terminal as the user types from keyboard,good for passwords masking.

#### Comparision operators
**And**: we use *and* to execute only when all conditions are true.represented with **&&** or **-a** or **&**        
**or**: we use *or* to execute when atleast one condition is true.represented with **||** or **-o**            
**;** we use it to end a command/line (not needed)        
       
| Description           | Numeric | String       |
| --------------------- | ------- | ------------ |
| less than             | **-lt** | **<**        |
| greater then          | **-gt** | **>**        |
| equal to              | **-eq** | **==**,**=** |
| not equal to          | **-ne** | **!=**       |
| less than equal to    | **-le** | N/A          |
| greater then equal to | **-ge** | N/A          |

we can view the result of comparision using "echo $?".      
Return value 0 means condition is true.If return value is 1 condition is false.                   
Numeric operator symbols(-lt,-gt) can only be used inside [],[[]].           
String operator symbols(<,>) can only be used inside (())                  

*Uses of brackets*
* [     ]: used to check conditions/perform operations.standard in posix systems.
* [[        ]]:extended version of [] used to perform additional operations like regex checks.
* (      ): used to perform commands that needs to run in a sub-shell
* ((     )):used to perform arithmetic mostly.        
both [] and (()) are used to perform arithmetic.       
>Ex: x=$[3\*3]  =>9         
> x=$((3\*3))  =>9        

### Command Substitution
To use terminal commands in our script we use backticks \`  \`.          
we place the command inside the backticks and store output in a variable.               

>Ex: list = \`ls -la\`;        

### Redirection
We can change the direction of output of a command/script.      
This is very powerful and used extensively for various purposes.               
standard output(STDOUT $0),standard input(STDIN $1),standard error(STDERR $2).               
**>**
used to redirect stdout to a file.overwrites data in the output file.               
**<**
take stdin from a file.                
* **>>**
used to redirect output of input command to a output file.appends data to a exisiting file.               
* **1>**
same as stdout               
* **1>>**
same as stdout with append               
* **2>**
redirects only errors of commands,can redirect to stdin using(2>&1).takes stderr and adds it to stdout.i.e displays on screen.
* **2>>**
same as stderr with append.               
* **&>**
redirects both stdout and stderr, equal to 2>file, 1>file. but prefer **&>** for both.               
* **|**
piping is taking output of one command and passing it as input to next command.               
* **tee**
redirects stdout to a file and shows it on screen.1> can't do this.
* **/dev/null** This is a null file in linux system,the file stores nothing,we throw our output into this null file if we don't need to display it.               


### Arithmetic operations
we can perform mathematical operations inside a bash script,it is done like this,      
1. No space before/after equal to.    
2. Define a variable using `let`.        
3. Quotes are optional,but recommended.    

we use following to define a integer and work with integers.     
* `let variableName = "mathematicalExpression"`
* variablename = "$[mathematical expression]"
* variablename = "$((mathematical expression))"
* always prefer with a dollar sign at the beginning to indicate it's a variable value.
* can prefix variables with 'expr' keyword to tell they are expressions.optional and have to escape * symbol. this will print the output.
>ex: all are valid        
>let x=3        
>let x="3\*3"        
>x="$[3\*9]"        
>x="$((3\*9))"        
>Ex: $(expr 3 * 5)      

**decimal arithmetic** all the above options can perform normal integer arithmetic operations,to perform decimal,float arithmetic operations we use "bc". this is a basic calculator in linux.
just pipe the expression to it for decimal calculations.         
>ex:echo "20.5 + 5" | bc    


### Relative vs Absolute path.
A file's location in a filesystem is the path of that file.       
To access a file in a linux system we use two methods.         
* **absolute** this means we access the file from the root directory,this is the easy one but very time consuming to code and debug. 
    1. '/' is root directory in linux,so if want to access a file in desktop we go from / to desktop,easy to code but is not portable,since each pc has a different desktop and user names.
* **relative** here we access the file from current location.
    1. './' is the current directory we are working in, we use this to move around in relation to the directory.
    2. '-' stores the last two directories we moved into,used as "cd -" to go to previous directory.
    3. '~' is the home directory of the current user,irrespective of the username.
    4. "../" go up a directory, can use this to move around the actual folder without referencing the root directory.


### Functions
Function is  a block of statements that are grouped together to perform a single task effeciently.            
A function is defined with the keyword "function" followed by the function name.                 
Alternatively can define a function with just a function name and (), i.e, functionname(){code}.              
We create functions to execute blocks of code multiple times,increasing reusability and giving better structure for our code. 
we call the function with its name/$name,can call another function inside a function.            
>Ex: function sysinfo(parameters) {            
>    date            
>    echo "printing current time and system info"            
>} $sysinfo/sysinfo            
>Ex: sysinfo(parameters){code}$sysinfo            
    


**local variables** all variables in bash are global variables,to specify a certain value as local we use keyword *local*      
**return** can't return values from bash,only execution status of the script,can return values from echo,printf etc,.         
**passing arguments** arguments are passed relative to their positions.To access arguments inside a function we use *$1 $2 $n* etc.,
* \$0 is reserved for function name/script name
* \$# gives number of parameters the function is given.
* \$\*,\$@ holds all the parameters in sequence, they differ when quoted/used inside a array.
* "\$*" returns values in "\$1 \$2 \$3" format,as a single string
* while "\$@" returns "\$1"   "\$2"    "\$3",as multiple elements.
> Ex:function f(){    
echo "hello $1"      
} f "hello" / f 'hello' 'h1'      

**readonly** the variable/function will be readonly so can't be modified,used for system variables.                 
We use -f to make items readonly.so can't be overwritten.         
**process number** can be printed with "$$"         


### Arrays
In bash arrays are either arguments user gives or sequence of data from a file.(with quotes)
The syntax to access arrays is $\* or $@ give data in a row,can assign it to a variable/array name.    
syntax to access array elements is ${arrayname[index]},{} is mandatory.
>Ex: array=("$*)      
>Ex: array=('a' 'b' 'c')      both are valid  
>echo ${array[0]}        

1. To remove items from array use **unset**
>Ex: unset array[2]
2. In bash strings are just a single item,not a array like C.So $1 in a string would be empty.

### Regex
Regular Expression is just a representation of automata.           
Denotes the pattern of text to search,it is used to search/identify text for filteration.           
Regex is mostly used with sed,java,python,bash and many more applications where a text file is being manipulated from a script,terminal.          

* In Regex everything is a character,if a sequence of characters(string) is given then  we search for that pattern,special characters has some specific meaning.
* **Character Classes**
  * "**.**" a wildcard character that can represent any character, digit,letter,whitespace in the text,except a newline.
  * [    ],characters inside square brackets are treated as individual characters,matched as it is.if only one character is given it will match all words containing that word.     
  * [azi] will match any letter from a,z,i in any order.   
  * [^abc] will not select a,b,c in any position of text
  * [a-z][A-Z][0-9] selects characters having any single value from the range at only a single position, unless global flag is specified,this will select pattern in all positions         
  * *\w* is used as a shorthand for [a-zA-Z0-9_] to match all english characters
  * *\W* matches everything except words 
  * *\d* is used to indicate digits, a single value from 0-9
  * *\D* matches everything except digits 0-9 
  * *\s* matches all whitespace except newline
  * *\S* matches everything except whitespaces
* **Anchors**
  * *^* selects all characters  at the beginning of a line.or multiple lines with multiline flag.
  * *$* selects characters at the end of line,or multiple lines with multiline flag.
  * *\b* selects charcters that have a boundary at the location,"\\bab" means this will select characters which have a space before ab.
  * *\B* selects characters that don't have a boundary,no space before or after character.
* **Escape characters**
  * '\\' is a escape character used to escape special characters that have a meaning or give normal characters like 't' meaning i.e, '\\t' which means tab.
  * '\\t' selects tab spaces.
  * '\\n' selects new lines
  * '\\r' selects return carriage(just like newline)
  * '\\.' prints a full-stop
  * '\\*' prints a asterik
  * '\\\\' prints a back-slash
* **groups & lookaround**
  * (abc) this is a capture group,matches exact group of characters,rather than combination of characters like [  ].this will match exact abc,not bca,bac etc.,.can reuse this group
  * \\1 reference to first group in a expression.
  * (?:abc) this is a non-capture group. can't reuse this.
  * (?=abc) positive lookahead matches group that has this after those characters.
    > t(?=es) in 'test' will only select t
  * (?!abc) negative lookahead doesn't match the characters with this group after them.
    > t(?!es) in 'testttttt' will select all t's except the 't' before 'es'
  * ** ** matches a space
* **quantifiers**
  * **\*** matches zero or more of a single character(kleen star)
  > aa* in "aaaaabbbbbbaaaa" will select all a's
  * **+** matches one or more of a  single character(kleen plus)
  > aa+ in "aaaaabbbbaaaa" will only select combination of aa's
  * **?** matches only zero or one of a single character
  > aaa? in "aaaabbbbbaaaa" will only select single  sets of aaa
  * **a{range}** matches repetition of a character
  >Ex:"aabbccaabbaaaab" a{1} will match single a's,a{1,5} will match atleast one a and max of 5 a's
  >[aze]{2,5} a repetition of 2 to 5 character that can be a mix of a,z,e in no particular order.
  * *ab|cd* used to represent "or" in pattern or group

### SED
Stream editor is used to edit text files.This is used to identify and perform operations on text in a file/given input.         
Created in 1970's,today used mostly for basic text manipulation operations.          
Can replace,insert,delete,search text in a file.            

Syntax:*sed -options 'operation/existing/extra-tags' file*         
1. **options**        
  In Sed the beginning letter in quotes is the operation to perform.         
  / is a delimiter,any extra tags,parameters can be given before the ending quote.          
  can use regex at "existing" for pattern matching.         
   * *-i* to edit the file with sed,normally just reads but this will edit the document and save it.
   * *-n* hides duplicate lines in output
2. **operations**
   * **most used** *s*-tag is used to substitute text,by default sed replaces the first occurence in a line   
   * **variables** we can use variables from shell in sed using *double quotes*.
   * Ex: sed "s/value/$variable/",with single quotes it takes as a literal value,not a variable.
    > s/n// in "hellohello" will remove the first h , substitue works with regex,then replaces those patterns with specified content,"s/pattern/newcontent/tags"            
   * *1-5* sed only takes effects in given range of lines,used before operation.
    > a specific line number(1st line),range of lines(1-5 5lines),(2-$ 2nd to last line).         
    > Ex: 2s/n// in "hellohello" will only take effect on second line of file.           
3. **extra-tags**
   * *d*-tag to delete a line in a file,line number can be (1 or 1-4 3-$),$ is last line.deletes lines given to it by the pattern.
     > Ex: "/^i/d" file, selects first line starting with i,then deletes it.         
   * *g*-tag global,applys pattern to entire page/file/paragraph,used in extra-tags place.             
   * *p*-tag prints the lines given to it.
       > '/regex/p' prints only lines matching the pattern           
   * *G*-tag insert blank line after pattern/line number

### Shell Flow Control
The power of any programming language comes from how they can use and manipulate data for a specific task.The data flow can be controlled,redirected depending on our need using one of the following methods.          
#### If
This is a conditional statement that executes commands if the condition inside is true, if it fails we can perform some backup commands.            
Follows operators rules,things to remember,       
* when using strings use [      ],
* when using values use ((      ))        
Syntax:        

      if[ expression ];(optional ;,mandatory spaces between condition and brackets)                
      then             
      commands                       
      elif[ expression ]--------->{to check multiple conditions}           
      then             
      commands           
      else---------------> {if no condition works then execute this}          
      commands         
      fi         
EX:
>if[ "$name" == "$USER" ]      
>then    
>echo hello $name      
>else         
>then        
>echo who are you?      
>fi       

##### Test
In flow control we can employ multiple conditional tests,most are user defined,some are system defined(existing) that can be used to enhance the flow.        
>use man test for additional details.     

most used system tests are         
* *-d* checks if the specified file is a directory.
* *-e* checks if specified file exists.
* *-s* checks if specified file's size is greater than zero(empty or not).
* *-w* checks if specified file has  write permissions.


#### Select
Select is like switch in c             
gives user option to select like 1,2,3,etc.,         
Select loop takes input from user and gives output from selected options.         
should write a break condition to exit(manually)         
Syntax:     

    select variable in list         
    do          
    case commands         
    done         

ex:
>select drink in tea coffee water juice exit           
>do           
>case $drink in           
>tea | coffee)---or---- tea/coffee)--->(can use |,/ to use **or** option){triggered when tea or coffee is selected}           
>echo "tea coffe"------>{any command}           
>;;--->{first case ending}           
>water)     ------->{another option to select}           
>echo "water"           
>;;           
>exit )        ---->(space between case and `)` is not mandatory,user preference)   
>break           
>;;           
>esac------>(ending the case conditions)           
>done           

##### case
Used to check multiple cases in a single code,like switch case in c.       
Difference between select and case is that select prompts user automatically for a numerical input,while case statements needs a variable given manually by user,more customizable.            
checks the expression/variable and searches for matching pattern/variable.        
If it matches than the commands in it will be executed.If no match is found a default * at the end will be executed.always use * as the last case condition as it matches any condition.
Syntax:  

    case expresssion in        
    pattern with regex/expression mathching )       
    command
    ;;-------->(to indicate commands end)       
    pattern )       
    command
    ;;       
    * ) --> (has to be at the end)
     command to execute if nothing matches
    ;;
    esac   ---->(case end)    

##### break
just like break in c,exits immediate loop when encountered.
##### continue
same as continue in c,skips all the code below it and goes to specified label or to start of the loop.

#### For loop
For is used to go through a list of items and perform tasks when condition is satisfied.              
For has many syntax's we use that are easy to use/better suits the needs.              
*Syntax:*    

    for variable in list;do commands done.              
    for variable in file file file; do commands done              
    for output in $(linux commands) do commands done              
    for ((int i;i<5;i++)) do commands done              

>Ex: for var in $(var list/variable file);do                   
>echo "$var"                   
>done     

Used to create automation scripts.     
prefer c like structure.    
lists can be used like 1 2 3 4 5 or {1..10..2}{start..end..increment} format.        

#### While loop
While is preferred when we don't know how many times a loop needs to execute.          
The loop will execute if the condition is true.         
The loop will get terminated if the condition is false.         
we can increment a variable as follows.          
>a = \'expr $a + 1` /  a=$((a+1)) /  a=$((++a))

**syntax:**

    while[condition]       
    do        
    commands       
    done       

Ex:
>while[ "$a" -lt 10 ]              
>do              
>echo $a              
>a = `expr $a + 1` / a=$((a+1)) / ((++a))              
>done              


* to involve a file in while's logic, we take help of input redirection.can only read normal files.any special character will be used in the code.
>Ex:while read p        
>do        
>comand        
>done < file        

* to read a special characters as normal character.we use IFS(internal field separator)
>Ex:while IFS=' ' read p         
>do         
>command         
>done < file         

#### Until loop
Until is opposite of while.         
It works as long as the condition is false and terminates once it is true.         
Since bash doesn't have a not statement in condition we use until.Ex:(!(x+5)=10) is not supported in bash.so for that we use until.         

EX:
>a=0          
>until[!"$a" -lt 10]          
>do          
>echo $a          
>a = `expr $a + 1`          
>done          

### Signal
when user presses **ctrl-c / ctrl-d / ctrl-z** it will interrupt the program execution.          
To execute code on these types of terminations we use signal. Their are many signals in bash that can be used to trigger a block of code.                   
use *man 7 signal* for all signal messages.          
### Trap 
Trap is used to perform tasks on signal raise,used with the signal number.         
As name suggests we use it to trigger a trap when a signal is generated.          
An example would be not letting the user press *ctrl-c* to terminate the process.         
Trap can be killed using **sigkill/sigstop** signal.         
>Ex:trap "commands to run" signalnumber/signalcommand        
>Ex: trap "echo script worked fine" 0;echo helo; exit 0;(0 is for successful execution)        
* can't stop sigkill,sigstop from terminal by trap.        


### Extras
* Typing a application name in terminal/script will start that applicatioln in that session,if the session ends so does the application.
* To continue execution of a application after the terminal session ends we use one of the following.
* giving '&' at the end of application start command will keep it running,in a new independent session from terminal.
* nohup COMMAND,(COMMAND &),setsid COMMAND works same with different pro's and cons.

**output of multiple commands**
To save output of multiple commands in to a single file we use grouping.                
just like a function with {   },all commands in a group will execute and their output is printed to a file if needed in sequential order.                
Ex:{echo "hello\n" echo "bye"} &>> somefile                


























