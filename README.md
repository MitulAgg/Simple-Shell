# Simple-Shell

This is implementation of custom shell in C . Here user can also run pipe commands along with feature of & foreground processes .

Key Components:
1.	Data Structure:
   
  ○	Data: It contain command in form of char** command where each element of array is command line argument , process ID, start time, and end time. 
  ○	Node: Node of a double linked list that contains Data.

2.	Node Management:
   
  ○	createNode(): Takes Data as input gives a node with previous and next pointing to null 
  ○	addNode(): Adds a new node to the end of the linked list.

3.	Command Execution:
   
  ○	command(): it is used for command without piping .
  ○	Executes a command using execvp().
  ○	It creates a child process that does the execvp(). 
  ○	If process is background(&) then parent does not wait() for child to finish execution else it uses wait(null)
  ○	In both cases commands data in added to the  linked list as history.

4.	Manual Command Parsing:
     
  ○	func(): The function takes command string as argument and splits it on basis of spaces and stores each string in char** args.

5.	Pipes Handling:
   
  ○	Pipe(): It handles commands that have piping in them.
  ○	It separates commands by | symbol and pass them to function then creates child process for each one
  ○	Parent process set up the pipes .
  ○	Child process executes each commands using execvp(). The input and output of child processes are directed by using dup2 commands
  ○	History of each child process is saved in Linked list.

6.	History:
   
  ○	printHis(): Displays the history in form of commands pid , start time , end time.
  ○	 The shell supports history with help of double linked list which stores process command ,pid ,start time,, end time in from of Data Struct .

7.	Main Function:
   
  ○	It takes input of command in an infinite while loop and checks if it is pipe or not ans uses command() and pipe() functions accordingly.
  ○	The loop terminates when the user enters exit, displaying the history before exiting.
