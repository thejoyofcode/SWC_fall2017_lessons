Software Carpentry Workshop: Lesson2: Linux shell
===
SWC workshop, November 2017
Instructors: Adnan and James
Time: 3 hours

## Linux environment
### 1. Why learn Linux?
+ Most widely used OS in research and technology
+ Open-source: free to get, free to use, free to modify.
+ Availability: Linux VM, Linux servers/clusters (UTA, TACC)
+ CLI (command line interface) and GUI (graphical user interface) are available

### 2. Bash as shell program to interact with Linux OS
+ We will focus on CLI that you can get access to through terminal window (open gitbash or terminal)
+ A shell is a command line interpreter for the system.
+ Bash is one of shell programs that can be used to interact with Linux OS. It is a program that runs other programs and it is also a programming language itself.
+ Let’s get familiar with the terminal first: prompt, commands, output
+ Here is the list of the commands we will use in the first half of the lesson. Not too many, but when used effectively, do simplify and speed up your work enormously!

``` shell
# commands used in this half of the lesson
$ echo       # print
$ whoami     # prints username
$ pwd        # print working directory path
$ cd         # change directory
$ mkdir      # make directory
$ touch      # create empty file
$ cat        # view file/concatinate files
$ mv         # move/rename file
$ cp         # copy file
$ rm         # delete file
``` 

Read-Evaluate-Print loop of CLI. When the user types a command and then presses the enter (or return) key, the computer reads it, executes it, and prints its output.

```shell=
# '#' here and everywhere should be interpreted as comment

# echo command is executed: Try
$ echo "Welcome to our workshop!"

# only commands known to bash will be executed: Try
$ stop this session 
```

{%pdfhttps://learncodethehardway.org/unix/bash_cheat_sheet.pdf%}

### 2a. Bash: navigate through your file system
Know who you are and where you are! Let’s talk about file system (folders and files) and how to find your way around …
```
# who am I? Try
$ whoami
```
And if I were to ask you where are you? Minimize your terminal for a second. You are back in your familiar GUI environment. Where are you? What folders are immediately available to you? Desktop folders? Open the terminal. Can you navigate to desktop using CLI?

```
# where am I? Try
$ pwd  
# this command prints your current location (or path to working directory) in the computer
```
Let's talk about what that output means.

**File system**: root, working, current, parent directories… 
![](https://i.imgur.com/6kKRSvQ.png)

> [name=AnnaWilliford] write a paragraph describing the figure! Introduce Folder==directory


Now, `pwd` command tells me where I am, but what is inside my working directory?
With GUI, all files are visible to you when you open a folder, but how do you see the files and/or folders in CLI?

```shell=
#list files
$ ls

#use flags to show different details: Try

$ ls -F

-F (file type) — Adds a symbol to the end of each listing. These symbols include /, to indicate a directory; @, to indicate a symbolic link to another file; and *, to indicate an executable file
# use man pages or --help to see what flags do what
# spend some time here - example of general command documentation
# 
# Option -a (all) — Lists all files in the directory, including hidden files (.filename).
$ ls -a


#Option -l (long) — Lists details about contents, including permissions (modes), owner, group, size, creation date, whether the file is a link to somewhere else on the system and where its link points.

$ ls -l

#Option -S (size) — Sorts files by their sizes

$ ls -S
# Do you have Desktop directory? You can list files present on Desktop: Try

$ ls -F Desktop  #if you do not have `Desktop` directory, it will give you an error...

```

#### Challenge 1

Remember, we made a `SWC_fall2017` folder in the beginning of workshop and moved our `Data` folder there. Can you now list files in SWC_fall2017 directory from your current directory?

#### Solution: 
```shell=
ls -F Desktop/SWC_fall2017/
```
####

In the exercise above, you viewed files in SWC_fall2017 directory while in home directory. But you can change the directory and move directly into SWC_fall2017 directory.

```shell=
$ cd Desktop
$ pwd
$ cd SWC_fall2017
$ pwd
# you could have done it in one step: 

cd Desktop/SWC_fall2017

$ ls -F
```
So, `cd` lets you change directories into daughter subdirectories. What if you need to go back?

```shell=
$ cd Desktop     #does not work, cd gets you into directories within current directory only

# But try this:
$ cd ..          #works

# Why? List all files in `SWC_fall2017` folder 
$ ls -F -a
```
`..` is a special directory name meaning “the directory containing this one”, or the parent of the current directory and `.` means “the current working directory”.


but `cd` without any arguments takes you ... where?
```shell=
$ cd

$ pwd
```

Relative vs Absolute Paths
Navigation with cd .. is an example of the relative path - you indicate where you want to go relative to the location you are currently in. When you give an absolute path to the folder or file, you will end up there no matter what your current location within file system is.

```shell=
$ pwd  #specifies absolute path


$ cd c/User/adnan/Desktop/SWC_fall2017

$ pwd  
#in my case `/c/Users/Adnan/Desktop/SWC_fall2017` is an absolute path to `SWC_fall2017` folder
```

Other shortcuts:
```shell=
$ cd ~ #takes you home
$ cd - #takes you BACK one directory, NOT UP!!!
```

#### Challenge 2
Mak
e a diagram of our directory structure (~/Desktop/SWC_fall2017/Data/) and practice navigation commands.

a) Find out where you currently are
b) Go to `Data` folder, what is there? 
c) Go back where you came from (with cd command)
d) Go one directory up
e) Try relative and absolute paths
f) get comfortable navigating across file system
####

### 2b. Bash: make new files and directories
Now that you know how to navigate your file system and list files that are already there, let’s see how we can create new folders and files.
You can create,delete,move,copy,rename files and directories using linux commands.

```shell=
#Navigate to `SWC_fall2017` folder
$ cd 

$ cd Desktop/SWC_fall2017
#check you are in the correct place

$ pwd

#create new directory for this lesson
$ mkdir unix_shell

#check
$ ls

#go to Linux directory
$ cd unix_shell

#now lets make two more directories here

mkdir India
mkdir Japan

#now check to see if you have these two directories in the folder

ls 

#create file
$ touch MyFirstFile.txt   # creates empty file
$ npp MyFirstFile.txt     # $ edit MyFirstFile.txt if you are on mac;  edit file

$ edit -w MyFirstFile.txt

$ cat MyFirstFile.txt     # view file
```
Open the MyFirstFile.txt in Notepad from GUI
Type:

"This is Software Carpentry Workshop"

Save and close it.

Now let's open the file in Bash:

```shell=
cat MyFirstFile.txt
```
You should see the line `This is Software Carpentry Workshop` in the terminal


Now lets try to rename,move, copy and delete files
```shell=
# move/rename file
# general syntax: mv $source $destination

$ mv MyFirstFile.txt MyFirstScript.sh

# Now try to move (but do not rename) MyFirstScript.sh to Japan folder
# you are currently in `unix_shell`

$ mv MyFirstScript.sh Japan/

# # check if MyFirstScript.sh is present in `unix_shell` and `Japan` without leaving `unix_shell`

# Copy file from `Japan` to `unix_shell`
# General cp syntax: cp $source $destination
$ cp Japan/MyFirstScript.sh .

#Now lets navigate to folder ‘India’
$ cd India/

#Now copy the file ‘MyFirstScript.sh’ to India
cp ../MyFirstScript.sh .

# Delete file !!! CANNOT BE UNDONE
# clean up `India`

$ rm MyFirstScript.sh  

# now lets clean up `unix_shell`
#go back to unix_shell
cd ..
#try to delete folders India and Japan

rm India
#deletes the folder

rm Japan
#does not delete the folder, gives an error message
#why?

#now use 
rm -r Japan/
```

#### Challenge 3

Next we will work with files from the `Data` folder that you moved to `SWC_fall2017` folder in the beginning of this workshop. Please move `Data` folder to unix_shell folder. We will keep all the files for Linux lesson in the `unix_shell` folder from now on. Make sure you understand the directory structure of SWC_fall2017 before we continue.



## Linux Lesson 2

Instructor: James 1.5 h
            
Time: 3 hours

### Lesson overview
#### Learning objectives:
- linux environment
- linux tools to manipulate text files
- shell scripts 
- working with multiple files

### 2c. Bash: manipulate text files**
Here is the list of the commands we will use in this second half of the lesson. Not too many, but when used effectively, do simplify and speed up your work enormously!
```shell=
# commands used in this second half of the lesson
$ wc         #word count
$ head/tail  #display start/end of file
$ cut        #extract fields(columns) of interest from file
$ sort       #sort file
$ uniq       #select uniq lines only
$ grep       #select rows based on content
```

Open `gapminder.txt` in your text editor first. Let’s understand this dataset.
You want to be able to get a feel for datasets like that usung command line interface. Some questions you might want to ask:

- How big is this file?
- What countries does this dataset include?
- What is the country with the highest life expectancy?
- What country has lowest population?
- How do these countries rank with respect to GDP?
- What year has the most data?

```shell=
#how big is your file `wc` outputs lines, words, bytes
$ wc Data/gapminder.txt  # try also with absolute path!

#look at the first 10 lines
$ head -n 10 .Data/gapminder.txt   # also try `tail`

##how many countries in this file? We will need more than one step here!
#1. extract the first column from the dataset:
#`cut` -  to get the column; `-f1` - flag to indicate we want the first column
$ cut -f1 .Data/gapminder.txt

#Let's redirect the output to file `CountryList.txt`; Use `>` operator to write to file.
$ cut -f1 .Data/gapminder.txt > CountryList.txt

#How can you view CountryList.txt? Notice that country names repeat many times!
$ cat CountryList.txt

#2.Sort and select uniq names only
$ sort CountryList.txt > CountryList_Sorted.txt
$ uniq CountryList_Sorted.txt > CountryList_uniq.txt

#the above 2 lines of code could be substituted with one:
$ sort -u CountryList.txt > CountryList_uniq.txt   # same as sort and then select uniq lines (sort|uniq)

#Is it correct? Header got in the mix - be careful!

#3. And finally, how many countries? 
$ wc -l CountryList_uniq.txt > CountryCount_gapminder.txt
```
What if we want more than one column?

We can do this by by listing the columns we are interested in.

```shell=
# Select botjh country and its resepctive continent.
$ cut -f1,2 Data/gapminder.txt > CountryYear.txt

# Or we can run it in a list
$ cut -f1-3 Data/gapminder.txt > CountryContinentYear.txt
```

Notice, we created 3 output files to find out how many countries are included into our dataset… Run `ls` to see for yoursef. Do we really need them? One way to avoid generating intermediate files you do not need is to string different commands together, known as ‘piping’

**Pipes**
Now let’s see how we can combine commands.
```shell=
# use `|` symbol to pass the output of one command as an input to the next command
$ cut -f1 Data/gapminder.txt | sort -u | wc -l > CountryCount_gapminder_2.txt

#a quick fix to avoid counting header as a country  # introducing `grep`
$ cut -f1 Data/gapminder.txt | grep -v "Country" | sort -u | wc -l > CountryCount_gapminder_3.txt
```

Now it is your turn…


**CHALLANGE 4**
What country had the highest "LifeExp" in 2012? 

Use `gapminder.txt` as an input file and generate `Country_HighestLifeExp.txt` as your ONLY output file.
Hint: you can accomplish this by using `grep`, `cut`, `sort` and `tail` but you might want to look up help pages for some of these commands...

**Solution:** first step by step and then as a pipe
```shell=
# 1. select all columns of interest - "Country", "Year", and "lifeExp.
cut -f1,3,4 Data/gapminder.txt > LifeExp_All.txt

#2. get data for 2012 only
grep 2002 LifeExp_All.txt > LifeExp_2002.txt

#3. sort by 3rd column from min to max
sort -n -k3 LifeExp_2002.txt > LifeExp_2002_Sorted.txt

#4. select country with highest mortality rate
tail -n 1 LifeExp_2002_Sorted.txt > CountryHighestLifeExp.txt

#Or as a pipe:
cut -f1,3,4 Data/gapminder.txt | grep 2002 | sort -n -k3 | tail -n 1 > CountryHighestLifeExp.txt
```

### 2d. Bash: write shell scripts
But what if you want to reuse these commands? You want to do something similar on another file? We need to save the commands to a file so we can easily reuse/modify them later. Such collection of commands in the order you want them to be executed is a simple shell script.

Copy and paste or just redirect the command that works (from the terminal) to `MyFirstScript.sh` file
```shell=
$ echo "cut -f1,3,4 Data/gapminder.txt | grep 2002 | sort -n -k3 | tail -n 1 > CountryHighestLifeExp.txt" > MyFirstScript.sh
```

We have just created `MyFirstScript.sh`. Let’s view and modify it slightly: `npp MyFirstScript.sh` or `edit MyFirstScript.sh` (if you are on mac)

- Add path to shell (bash in our case) that will execute your code; should be your first line: `#!/bin/bash`
- Add description of what script does.
- Add usage statement: `#usage: script.sh`

Let’s run it. But first look at it carefully, do you think it will run?
`#./ indicates that you are running script from working directory
./MyFirstScript.sh`

Well, it runs and generates the expected output. But is it a good script? Could you reuse it with a different file as input file? How can we make it more flexible?

To make it flexible we need to inroduce a variable for a part of the code that we want to change frequently. For example, if we want to run this code with a different file, we want a variable instead of hard-wired filename; a variable can take any user-defined value.

**Variables in bash**
Varible name: myName; value assigned to it: Your Name
```shell=
#try this
$ myName=James  #variable assignment
$ echo James  
$ echo myName
$ echo $myName  # need `$` to get the value of the variable
```
Let’s modify MyFirstScript.sh to include a variable and save it as MyFirstScript_2.sh Also change the name of the output file to CountryHighestLifeExp_2.txt so that we can be sure that the output corresponds to this new modified script.

Here is MyFirstScript_2.sh
```shell=
#!/bin/bash

#record a country with highest Infant_mortality among countries in OECD_Countries_Full.txt
#usage: script.sh

input=Data/gapminder.txt

cut -f1,3,4 $input | grep 2002 | sort -n -k3 | tail -n 1 > CountryHighestLifeExp_2.txt
```

Run it: `sh MyFirstScript_2.sh`

Is it better? A little bit… why? What would be even better? We want to provide filename at the command line and not have to change the script itself.

Here is MyFirstScript_3.sh
```shell=
#!/bin/bash

#record a country with highest Infant_mortality among countries in OECD_Countries_Full.txt
#usage: script.sh $inputFile   #notice how we need to run this now

input=$1  #special variable that stores the the first argument from the command line

cut -f1,3,4 $input | grep 2002 | sort -n -k3 | tail -n 1 > CountryHighestLifeExp_3.txt
```

Run it: `sh MyFirstScript_3.sh gapminder.txt`

Is it better? Why? Can we make it even better? How?

**CHALLANGE 5**
Work in groups to write a script (name it `MyFirstScript_Good.sh`) that would allow user to compare any indices between the countries (not just lifeExp), use data for any year (not just 2002) and write the output to a user-defined output file.

**Solution:**
Here is MyFirstScript_Good.sh
```shell=
#!/bin/bash

#record a country with highest Infant_mortality among countries in OECD_Countries_Full.txt
#usage: script.sh $inputFile $index $year $outFile   #notice how we need to run this now

input=$1              #special variable that stores the the first argument from the command line
columns=$2            # $2, $3, $3 store values from 2-4 command line arguments
year=$3
out=$4

cut -f1,3,$columns $input | grep $year | sort -n -k3 | tail -n 1 > $out

```
Run it: `sh MyFirstScript_Good.sh gapminder 5 1982 LargestPop1982.txt`
This is much better!


#### Passing command line arguments to shell scripts
...

You have seen how we can run shell scripts from the command line. But remember that the shell is the environment for running any scripts/programs. We can just as easily run R script we wrote this morning.

```=
#to run from command line
$ Rscript PlotLifeExp.R
```


***Transition to next lesson***

You have seen how we can use Linux environment to run bash and R scripts. You can run scripts written in any programming language in a similar way. And you also can run R (or any other)scripts from within shell scripts! Such combination of Linux commands with R scripts can be very effective. We will see the example of this tomorrow after we learn more about R programming.
