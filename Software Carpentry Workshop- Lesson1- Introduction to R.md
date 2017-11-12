Software Carpentry Workshop: Lesson1: Introduction to R
===


SWC workshop, November 2017
Instructors: Farah and Balan
Time: 3 hours

---
Good morning!
Before we start working with R, let's make a folder where you will save all your work during this workshop.

Let's make a folder `SWC_fall2017` on your Desktop. We will be working with this folder for the next 2 days so it is better if you leave it on the Desktop where it is easily accesible. It also helps for everyone to have the folder in the same location as it will make it easier to navigate to your files when we start using command line interface later today.

- [x] do it with students and make sure everyone is with you - put up red sticky notes if having problems, green when done with the task. 

Now let's download datasets (Data.zip) for the workshop and put it in `SWC_fall2017` folder.

https://raw.githubusercontent.com/AnnaWilliford/2017-11-11-UTA/gh-pages/workshop/SWC_fall2017/Data.zip

When you unzip this file, you should have `Data` folder with `ByCountry` folder and `gapminder.txt` file in it.


Finally, let's make another folder called  'R_intro' inside `SWC_fall2017` folder. This is where we will save all files for this lesson.

- [x] do it with students and make sure everyone is with you - put up red sticky notes if having problems, green when done with the task.


Now we are ready to work with R!


### Learning objectives
- Understand benefits of using R
- Understand how to work with RStudio
- Understand how to go get data from Excel to R
- Understand building blocks of R language
- Understand how to extract parts of the dataset
- Understand how to write simple R scripts

## 1. Intro to R and RStudio

###  Why R?

* Statistics, graphics, general purpose programming
* Thousands of packages available - these are collections of functions that implement all kinds of analyses of data sets from various disciplines
* Open source software - use for free, modify as you wish
* Active community of developers - new packages are being written as we speak

### RStudio as interface for R(IDE - integrated development environment)
We will be working with R using RStudio. This is a piece of software (also known as integrated development environment, IDE ) that makes working in R much easier. When you open RStudio, you should see 4 windows:

* The 4 windows of RStudio:
    * Top left = text editor,write your commands/code here
    * Bottom left = R console, run (execute) your commands here
    * Top right = things that R keeps track of:
        * History tab records all the commands you type in R console
        * Environment tab keeps track of all objects you create in the current session
        * Both records can be saved for later as .Rhistory and .RData files
    * Bottom right = several helpful tabs, we will see how to use them later. For now, notice that 'Files' tab allows you to navigate between folders.
          For this workshop we need to navigate to 'SWC_fall2017' folder that we created on the Desktop. Click three dots icon at the top right corner of the 'Files' tab and navigate to Desktop/SWC_fall2017. We want to enter 'R_intro' folder. When there, click 'More' and select 'Set as working directory'. Notice the change in your console window  - your work with R is now done from 'R_intro' folder.
         - [x] do it with students and make sure everyone is with you - put up red sticky notes if having problems, green when done with the task.

* Interactive mode. When you type commands in the console window and press 'ENTER', they are executed immediately and the output is displayed. Here are few examples:  
            > 3+5
            > sqrt(64) 
            > print("How are you?")
            
    Symbol `>` means that the R is ready for the next command. If you enter incomplete commands, you will see `+` which means that the system is waiting for you to complete the command. You can always press 'Esc' to return to `>` when stuck with `+` at the prompt.
        
* Scripting mode. It is often the case that we would like to reuse our commands. If so, you can type commands in the text editor window. Let's open a new R Script file and write our command there, for example `print("Good morning!"`). To check if this command works, you can send it for execution to console with 'CTR +Enter' click. We have a very simple example here, but you can imagine writing hundreds of commands in the order you want them to be executed to accomplish a certain task. This is what an R program or R script is. It is a good practice to comment your code. The comments (statements that are helpful to the user, but are not seen by R as commands to be executed) in R start with `#`. Let's add a comment to our simple script.

    ```
    #my first R command 
    print("Good morning")

    ```
    We can save the file with our commands and reuse it later. For now, let's save our example as R_commands.R in R_intro folder.
    
    - [x] do it with students and make sure everyone is with you - put up red sticky notes if having problems, green when done with the task.
    

## 2. Building blocks of R

Let's work in scripting mode from now on so that you will have the record of all commands we used in this lesson.

### Variables/objects

One of the main concepts of any programming language is a notion of a variable. Variables are created to store values for future use.
To create a variable in R, use `<-` (Alt + dash) assignment operator:
```
### Variables

#variable name that stores value "Jane"
name <- "Jane"
print(name)

#variable price that stores value 3.99
price <- 3.99
print(price)

```
**Challenge 2.1**
    
```
TASK: What will be the value of each  variable  after each statement in the following code?

mass <- 47.5
age <- 122
mass <- mass * 2.3
age <- age - 20
height <- height + 20
        
```

As you can see, a variable is assigned a value equal to the value of the evaluated expression on the right side of the assignment operator. 

**A note on variable names:**
* NO SPACES in names
* DO NOT START with numbers
* Names should be MEANINGFUL - help yourself and others to understand your code! 

Every time you assign a value to a variable, you create a new object. You can see what objects you create if you look at the 'Environment' tab of the top-right window of RStudio. The objects you create are in your environment until you remove them. You can manage your environment in the following way:
```
### working with environment

#list all objects in your environment
ls()

#remove object objectName
rm(objectName)

#remove all objects, clear environment
rm(list=ls()) 
```

### Functions

In general, a function takes an input and transforms it according to the function's definition(rules). You can recognize functions in R by the presence of parantheses. Objects in parantheses are called function's **arguments** 
```
### Functions

#applying square root function
mass<-64
res<-sqrt(mass)

#applying getwd() function
getwd()
```

In the fist example, the square root function takes `mass` object as input and finds the square root of its value. The result is then assigned to `res` variable. In our second example, `getwd()` is a function that outputs your current location within the file system. Although there is no input (many functions do not require arguments), parantheses are still required for a proper syntax in R.

There are thousands of built-in functions in R. There are also help functions that you can use to find out what other function do and how to use them. The help appears in the bottom-right window of the RStudio.

```
### helpfunctions

?plot
help(mean)
```
The functionality of R is expanded by R packages that include functions not present in the default installation of R. When you need to use another package, do these 2 things

```
### working with additional packages 

#install package called "knitr"
install.package("knitr") 

#load package into R
library(knitr)
```
### Data types and Data structures


#### Smallest units in R: single-element data structures

Let's assign value of 45 to a variable `age`. We just created the smallest object in R:
```
age <- 45

#some useful functions to know more about the object 
length(age)
str(age)
```
Variables can hold values of various types. Most common data types:

* numeric(double+integer)
* character
* logical
* complex
* ...

For example: What data type is stored in `score` variable?
```{r}
score<-79
is.integer(score)
typeof(score)
typeof(is.integer(score))
```
The last expression is an example of nested function. Nested functions are very common in R, but are very difficult to understand at first. You can always split nested function into a series of single function calls. Remember that the variable inside the most inner paranthesis is an argument(input)for the function that will be evaluated first.

**Challenge 2.1:** Learn how to read the output of nested help functions
```
TASK: Break the following expression into multiple single function calls.
You will need to assign the output of each function to a variable that
will serve as an input(argument) for the next function. 
What is the value of each variable? What does each function do? 
Assign: `score<-79`

is.logical(is.numeric(typeof(is.integer(score))))
```
**Challenge 2.1: Answer**

> ```
> score <- 79
> step1 <- is.integer(score)
> print(step1)
> step2 <- typeof(step1)
> print(step2)
> step3 <- is.numeric(step2)
> print(step3)
> step4 <- is.logical(step3)
> print(step4)
> ## Or as a single step:
> print(is.logical(is.numeric(typeof(is.integer(score)))))
> ```

Sometimes you will need to convert between data types. There are functions that do that: as.integer(), as.character(), and so on. The conversion between data types is not always possible - why? Let's see what happens here:

```
score <- 79
typeof(score)
score <- as.integer(score)
typeof(score)
#but can we convert character to integer?
name <- "Sasha"
typeof(name)
name <- as.integer(name)
# the data type will be changed, but no value will be assigned
typeof(name)
print(name)   # NA = missing value
```


#### Data structures with multiple elements
The small objects can be combined to build larger objects. Look at the gapminder dataset again. Our smallest objects can be used to represent a single element in the dataset, like individual year, or individual country, but what would be the simplest object that you can make with multiple elements?

* Vectors: collection of elements of the same data type
    * what part of our dataset can be represented by a vector?
    * how to create: use concatinate function, c()
    ```
    ###let's make a vector
    v<-c(1:3, 45)
    v

    #examine object
    typeof(v) # tells you the data type of vector elements

    length(v) # what does this do?

    str(v)    # tells you the structure of the object VERY USEFUL

    #view
    head(v, n=2)  #look at the first 2 elements

    #what would `tail()` do?
    tail(v, n=3)  #look at the first 3 elements

    #manipulate
    v <- c(v,56)  #add element to vector
    
    #vectorizarion 
    v1 <- 2*v   # multiply each vector element by 2
    v1

    # let's try to add vectors
    v2<-c(1:5)
    v3 <- v1+v2
    v3

  
    # change data type
    v3 <- as.character(v3)  #also known as coersion
    str(v3)
    ```
* Matrices: 2-dimensional vectors that contain elements of the same data type
    * how to create: use matrix() function
    ```
    m <- matrix(c(1:18), 3,6)
    m
    # try functions that we used for vectors - do they work on matrices?
    # new to 2D structures
    dim(m)  # tells you number of rows and columns in your matrix
    ```
* Factors: special vectors used to represent categorical data
    * what part of our dataset can be represented by a vector?
    * to create: use factor()
    ```
    ## 4 observations, the first one for male, other 3 for female
    f <- factor(c("M","F","F","F")) 
    str(f) # what are these numbers in the output?
    typeof(f)   # factors are of integer data type! Levels are numbered in alphabetical order
    #sometimes important to reorder levels
    f <- factor(f, levels=c("M","F"))
    str(f)
    ```

* Lists : generic vectors - collection of elements with different data types
    * what part of our dataset can be represented by a list?
    * to create: use list() function
    ```
    l<-list("Afghanistan", 1952, 8769855)
    print(l)
    typeof(l)
    str(l)
    length(l)
    ```
     **CHALLENGE 2.2** 
    
    ```
    TASK: Try to create a list named 'myOrder' that contains the 
    following data structures as list elements:

    -- Element 1 is a character vector of length 4 that 
    lists the menu items you ordered from the restaurant: 
    chicken, soup, salad, tea.

    -- Element 2 is a factor that describes menu items
    as "liquid" or "solid".

    -- Element 3 is a vector that records the cost of each menu item:
    4.99, 2.99, 3.29, 1.89.

    *Hint: Define your elements first, then create a list with them.
    ```
    **CHALLENGE 2.2: Answer**
    
    > ```
    > menuItems<-c("chicken", "soup", "salad", "tea")
    > menuType<-factor(c("solid", "liquid", "solid", "liquid"))
    > menuCost<-c(4.99, 2.99, 3.29, 1.89)
    > myOrder<-list(menuItems, menuType, menuCost)
    > ```
        
    Now apply the following functions to the list you created. Try to predict the output before you run the command.
    * length(myOrder)
    * str(myOrder)
    * print(myOrder)
        
* Data frames
    * Let's go back to gapminder dataset. Could you make an informative guess about how this data structure can be represented in R?

    * Yes! It is a list of vectors of equal length, or a data frame. Data frames are extremely useful data structures as they represent table-like datasets. Let's look at our myOrder list to see if we can make data frame out of it. Is the list we just made suitable for a data frame? Yes, the elements of the list are vectors of equal size.
    
    Previously we used list() to combine our elements:

    * `myOrder<-list(menuItems, menuType, menuCost)`
    
    Now let's combine with data.frame() function. How? Give it a different name, myOrder_df.

    ```
    myOrder_df<-data.frame(menuItems, menuType, menuCost)
    
    #now view it!
    myOrder_df

    #and check with str()
    #anything different compared to str(myOrder)
    #output? What is happening with data types? 
    
    str(myOrder_df)
    ```
### General subsetting rules

Now let's talk about how to take your dataset apart. In general, you can access every element of your data set. You must be able to do that to manipulate and analyze your data. There are three general ways to subset the data:

```{r}
### 1. By position index: Use [] operator

v<-c(1:10)
v

## see what happens here
v[2]
v[c(3:6)]
v[-c(3:5)]


## the above works for lists too, notice that [] returns list, use [[]] to return vector
## try subsetting myOrder list we created above
myOrder[1]
myOrder[[1]]

##for 2D structures like matrices and dataframes provide 2 indices [row, column]
myOrder_df[1:3, ] #gets first 3 rows

### 2. By name:
# For lists and dataframes: use `$` operator to extract columns as vectors 
myOrder_df$menuType

### 3. By logical vector index: selects elements corresponding to TRUE values 
### of logical vector:###
#####################################
# >  greater than
# < lesser than                   
# == equal to
# >= greater than or equal to
# <= lesser than or equal to
#####################################
v<-c(1,5,3,4,5)

#select elements that equal to 5
v1<-v[v==5]
v1

# how does the above work? Try:
v==5   # returns logical vector
#v[v==5] selects element of v that have TRUE values in the output of v==5

##Use `myOrder_df` dataframe:select rows that satisfy various conditions
##Diplay logical vector to understand the ouput
df1<-myOrder_df[myOrder_df$menuType=="solid", ]
df1

df2<-myOrder_df[myOrder_df$menuCost>3, ]
df2

##Can you explain the output generated here?
df3<-myOrder_df[myOrder_df$menuType=="solid"]
df3

```
Subsetting and tearing apart the statistics;

## 3. Overview using our gapminder dataset

Let's return to our gapminder dataset.

Before we examine our data, let's read(load) this dataset into R. There are multiple ways to read data into R. For table-like formats, there are 2 popular functions:

* 1. Use read.table() function
    * myData<-read.table("gapminder.txt", header = TRUE)
    * Take a look at the new object myData
    * A bit hard to see? It is too large to be displayed at the console. Different ways to see what your object looks like:
        * Use head() function:
            * head(myData)
        * Look at the top right window, environment tab - gives you a brief summary of the object and opens an Excel-like view of the dataset
        * always check that you read in a complete data set `dim(myData)` to see if you have the correct number of rows and columns
* 2. Use read.csv() function
This function is for .csv files (where fields are separated by a comma)

Now we know how to read dataframes into R. Let's use R to find out more about the data

**Challenge 3.1**  Play with gapminder dataset

```
TASK: Answer the following questions about `myData` object
1. What is overall object structure? What function will you use?
2. Can you tell the data type of the elements in each column?
3. Can you extract 3rd and 5th column of the dataset?
4. Can you extract the list of countries in this dataset?
### Hint: use unique(). ###
5. Can you get a part of this dataset that includes information about Sweden?
6. Can you extract all countries for which life expectancy is below 70?
7. Can you make a new column that contains population in units of millions of people?
```
**Challenge 3.1: Answer**

> ```
> 1. str()
> 
> 2. typeof() 
> Will return "list" because
> dataframe is a list of vectors; examine the
> output of str() for details about column data types
> 
> 3. myData[ ,c(3,5)]
> You can use head(myData[ , c(3,5)]) to view
> top 6 rows of the output
> 
> 4. unique(myData[,1]) 
> 
> 5. myData[myData$country=="Sweden", ]
> Here, rows are selected based on logical 
> vector TRUE values - can you view this vector?
> 
> 6. myData[myData$lifeExp<70, ] #similar to Q5
> 
> 7. myData$PopM<-myData$pop/10^6  
> This is a simple way to add a column to a dataframe. 
> You can verify that you added a column with head(myData)
> ```
## 4. Writing simple R scripts

An R script (or any other script) is a series of commands that are executed in the order they are written. The commands that we have executed one by one in R studio can be written to a text file and then executed all at once by running the file (which is now an R script). R scripts usually have .R extensions. Here is an example of a simple R script that will plot life expectancy over years for Canada. 

```{r}=
##This is  PlotLifeExp.R script

#read data into R
myDataFull<-read.table("gapminder.txt", header = TRUE)

#myDataFull is a dataframe - check

#select information about Canada
Canada<-myDataFull[myDataFull$country=="Canada",]

#Canada is a new dataframe

#plot lifeExp 
plot(Canada$year, Canada$lifeExp, col="blue", type="l")
```

To run this script from R studio (or R):
```=
source("PlotLifeExp.R")
```
You might want to save your plot as .png image. This requires only slight modification of our script.
```{r}=
##This is  PlotLifeExp.R script

#read data into R
myDataFull<-read.table("gapminder.txt", header = TRUE)

#select information about Canada
Canada<-myDataFull[myDataFull$country=="Canada",]

#plot lifeExp 
png("Canada.png")  #open png device to write your plot to 

plot(Canada$year, Canada$lifeExp, col="blue", type="l")

dev.off()  #close device; Canada.png will be saved to your current folder (R_intro)

```
**Challenge 3.2**  Write your own R script
```
Write a script to calculate mean gdpPerCap for African and European countries.
Try to make a barplot to display your results.

You might need to read help for 'mean' and 'barplot' functions
?mean
?barplot
```
**Challenge 3.2: Answer**
```{r}=
##This is  MeanGdpPlot.R script

#read data into R
myDataFull<-read.table("gapminder.txt", header = TRUE)

#select information about Africa
Afri<-myDataFull[myDataFull$continent=="Africa",]

#calculate the mean 
Afri.Mean <- mean(Afri$gdpPercap)

#Do the same for Europe
Europe<-myDataFull[myDataFull$continent=="Europe",]
Euro.Mean <- mean(Europe$gdpPercap)

#Store the mean values in a vector
Afri.Euro.Mean <- c(Afri.Mean, Euro.Mean)

#plot MeanGdp
#open png device to write your plot to 
png("Afri.Euro.Mean.png") 

continents.names <- c("Africa","Europe")

barplot(Afri.Euro.Mean, names.arg = continents.names, col = c("#a8ddb5","#43a2ca"), xlab = "Continents", ylab = "Mean GDP per Capita")

dev.off() 
```

***Summary***

This lesson introduced you to main ideas of programming: variables, functions, data structures and scripts. Now you can write your own simple programs in R and begin understanding R code written by others. Before we continue with R tomorrow, we need to introduce a different tool- Unix shell. Shell is a program used to interact with Unix/Linux operating systems. It is essential to know how to work with Linux because at some point your analysis will require more computing power than your laptop can offer, and you will move your work from local machines to computer clusters most of which are running Unix/linux operating system. In addition to providing a more suitable environment to run your analysis, Linux offers multiple tools (short programs) for very efficient manipulation of text files.