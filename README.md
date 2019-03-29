
# UNIX Shell Implemented in C
This program simulates the working of command line interface in Unix-like environment. Functionalities implemented:

- Execute all(except sudo) external commands (ls, clear, vi etc.)
- Implement internal commands: cd, pwd
- Initialization and use of environment variables
- Print environment variables using echo command
- Redirection operators: STDIN, STDOUT, STDERR (>>, >, <<, <, 2>) 
- Support for history command and '!' operator (history, !!, !-1, !10,!-10 etc)
- Pipes "|"" (multiple) (Ex: ls | grep 'a' | wc)


# Input/Output Format

Input from 'stdin' in an infinite loop till an explicit "exit" is entered.
The corresponding output is printed to 'stdout'.

Ex:
assume that PWD == /home/user
bash prompt:~$ ./a.out
nikhil@shell:/home/user$ ls
shell.c history.txt a.out
nikhil@shell:/home/user$ gfhj
gfhj: command not found
nikhil@shell:/home/user$ exit
Closed
bash prompt:~$


# Implementation Details

The shell.c contains the main function which takes the input from user and checks it for pipeline. If pipeline exist it processes the data separately, otherwise it passes the data to the functions. The shell.h contains all the function prototypes.

## int with_pipe_execute():
This function is the initial function which is called for checking the all the command after initial preprocessing is done. It passes the processed output to function split.

## int split(char *cmd_exec, int input, int first, int last):
This function is responsible for splitting of command and passing it to command function.

## static int command(int input, int first, int last, char *cmd_exec):
This does the major part of the program. It checks for various possibilities of commands. The types of commands that are checked :
1) Internal commands: pwd and cd
2) echo commands, setting and getting environment variables
3) redirection handler 
4) PIPE
5) External commands

It makes use of various functions like tokenise_redirect_input_output, tokenise_redirect_input, tokenise_redirect_output which internally calls tokenise_commands() for tokenization.


## Helper functions:
- getcwd():
gets the current working directory

- signal():
Handles interrupt signals

- void prompt():
initiates new prompt 