bash is the basic programming languages that is used for giving input to kernel.
The Shell(sh) is the first one to be used by programmers.
after that came ksh,csh for various niches and purposes then came bash(bourne again shell).
Bash being backwards compatible and POSIX   standard compliant became wide spread and now is everywhere.
It's the default shell in most linux distro's and mac os.(unix based)
have some better features than older shells but still is designed in the 80's so was not updated that often.
So developers forked it and created multiple shell's now we have many shell's for various purposes.
Zsh(z shell) is the most famous one, designed in 2000's but is only used by specific group.
It's backwards compatible with bash(hence popular).
But we still create scripts in bash(.sh).

terminal is short for terminal emulator and is just a interface for the user to give input and pass that to corresponding shell.
The shell does the work and returns the output to user(terminal)
then the shell waits with a prompt to enter another command.
EVery thing we do in a terminal, where ther input is text based and output is text based is a command line interface(cli)
the data we pass with a command is command line arguments.

Commands for terminal:
echo(to print content on screen)we can used double quotes to enclose the content to print or just give the content itself.
read(to take input from the user)
ls(list files)
cd(change directory)
    cd ..(up a directory)
    cd (home directory)
    cd ~(home directory)

pushd(to go in a directory)
popd(to go back to first directory)for ease and not remembering the direcotry place
file(to check the type of file)
locate(search for a file)(need to update database)
    sudo updatedb
which(searching the location of a package/program)
history(shows the last 1000lines of commands run in the terminal)
whatis(used to get the introduction of a package/program)
apropas(to search for a package with relevant to given input)
man(to read the manual pages of package/command, shows how to use)
cp(copy first file into second file)
mv(used to move files and rename)takes first file and keeps it in the second place
rm(powerful, removes files and directories)
glob(* in the command that fills and searches is glob,? searches only one character)
rmdir(used to remove empty directories)
cat(used to concatenate read and add text to files)(small files)
    > filename(will create a new file/overwrite extending exisiting one)
    >> filename(will add to the end of file)
more(text reader that shows document in page order with space button)
less(advanced than more command can use arrow,space,search for)
nano(text editor in terminal)
|(piping taking output from one program, giving it to the input of another program)
chmod(changing permission for user,group,everyone to give read(4) write(2) execute(1) access.)chmod 755 or +x
killall(kills the process name given)


Bash Scripting:
just creating a file with all the commands to perform on execution is scripting.
we can use multiple shells for scripting.

most common and wide spread is bash can have extension .bash, or .sh

Shebang:
#!/bin/bash
this is used to tell the interpreter which shell to use
# sign is used to do comment out code in script
run with the command(the file need to be executable) chmod +x file.sh
bash file.sh(or)
./file.sh(only works on native drive, may not work in mounted drives)

Variables:
str="value"
echo $str
{can give text,numbers,path}
accessed with $variablename

Command Substitution:
taking the output of shell commands and assigning them to variables
lsit=`ls`
we use backticks, so the interpreter takes it as a command
the output is given to the variable

Arithmetic operations:
to perform mathematical operations in bash we use one of the following

(quotes are optional)
let variablename = "mathematical expression"

variablename = "$[mathematical expression]"
variablename = "$((mathematical expression))"

ex:
let x = "10*2+3"
x = "$[10*2+3]"
x = "$((10*2+3))"

expr value/variable +,-,/ value/variable
we use it mostly for loops(increment/decrement),space is needed for calculation

Shell Controlling:
Loops:

While loop:
to execute certain group of commands, certain number of times.we use loops, while is the most used one.
while works as long as the condition is true. stops after it is false
**syntax:**
while[condition]
do 
commands
done

Ex:
while["$a" -lt 10]
do
echo $a
a = `expr $a + 1`
done

Until loop:
Until is opposite of while, it works as long as the condition is false and fails once it is true
EX:
a=0
until[!"$a" -lt 10]
do
echo $a
a = `expr $a + 1`
done

For loop:
for does what while does but some more features like array reading,file reading,auto increment/decrement
ex:
for var in 0 1 2 3 4 5 
do 
echo $var
done

for file in /etc/n*
do
echo $file
done

select loop:
select is like switch in c
select loop takes input from user and gives output from selected options.
should write a break condition to exit(manually)

ex:
select drink in tea coffee water juice break
do
case $drink in
tea|coffee)              {triggered when tea or coffee is selected}
echo "tea coffe"        {commands}
;;                                  {first case ending}
water  )                         {starting another option}
echo "water"
;;
exit)
break
;;
esac(ending the conditions)
done

If:
this is a conditional statement that executes commands if the condition inside is true, if it fails we can perform some backup command also.
syntax:{need space after [ and before ]}
if[expression];
then
commands
elif[expression];{to check multiple conditions}
then 
commands
else{if no condition works then execute this}
commands
fi
ex:
if[ "$name" = "$USER" ];
then
echo hello $name
else
then 
echo who are you?
fi

extra commands to check
-d variable{checks if the path is directory }
-f variable{checks if the path is  file }
-e variable{checks if file exists}
Environmental variables:


































