Software Carpentry Workshop: Lesson3: R programming
===
SWC workshop, November 2017
Instructors: James Titus-McQuillan
Adapted from Rohit Rawat
November 12, 2017

Time: 1.5 hours


**Lesson Overview**
We have covered basic R usage:
- Reading data files
- Creating and manipulating variables
- Data types
- Calling built-in functions

Now we will cover:
- Writing functions
- Scope issues in functions, Missing arguments
- Calling R scripts from the command line


## Creating Functions
Functions are “canned scripts” that automate something complicated or convenient or both. Many functions are predefined, or become available when using the function `library()` (more on that later). A function usually gets one or more inputs called arguments. Functions often (but not always) return a value. A typical example would be the function `sqrt()`. The input (the argument) must be a number, and the return value (in fact, the output) is the square root of that number. Executing a function (‘running it’) is called calling the function. An example of a function call is:

`b <- sqrt(a)`

Functions gather a sequence of operations into a whole, preserving it for ongoing use. Functions provide:
- a name we can remember and invoke it by
- relief from the need to remember the individual operations
- a defined set of inputs and expected outputs
- rich connections to the larger programming environment

Let’s create a new script, call it functions-lesson.R, and write some examples of our own. Let’s define a function `fahr_to_kelvin` that converts temperatures from Fahrenheit to Kelvin:

```shell=
fahr_to_kelvin <- function(temp) {
  kelvin <- ((temp - 32) * (5/9)) + 273.15
    kelvin
}
```

The definition opens with the name of your new function, which is followed by the call to make it a `function` and a parenthesized list of parameter names. You can have as many input parameters as you would like (but too many might be bad style). The body, or implementation, is surrounded by curly braces `{ }`. In many languages, the body of the function - the statements that are executed when it runs - must be indented, typically using 4 spaces. While this is not a mandatory requirement in R coding, we strongly recommend you to adopt this as good practice.

When we call the function, the values we pass to it are assigned to those variables so that we can use them inside the function. The last line within the function is what R will evaluate as a returning value. For example, let’s try running our function. Calling our own function is no different from calling any other function:


```shell=
fahr_to_kelvin(32)

## [1] 273.15

print(paste('boiling point of water:',fahr_to_kelvin(212)))
## [1] "boiling point of water: 373.15"
```

We’ve successfully called the function that we defined, and we have access to the value that we returned.
```shell=

fahr_to_kelvin <- function(temp) {
  kelvin <- ((temp - 32) * (5/9)) + 273.15
    kelvin
}
```

**Composing Functions**
Now that we’ve seen how to turn Fahrenheit into Kelvin, it’s easy to turn Kelvin into Celsius:
```shell=
kelvin_to_celsius <- function(temp) {
    Celsius <- temp - 273.15
    Celsius
}

print(paste('absolute zero in Celsius:', kelvin_to_celsius(0)))
```
```
## [1] "absolute zero in Celsius: -273.15"
```

What about converting Fahrenheit to Celsius? We could write out the formula, but we don’t need to. Instead, we can compose the two functions we have already created:
```shell=
fahr_to_celsius <- function(temp) {
    temp_k <- fahr_to_kelvin(temp)
    result <- kelvin_to_celsius(temp_k)
    result
}

print(paste('freezing point of water in Celsius:', fahr_to_celsius(32.0)))
```
```
## [1] "freezing point of water in Celsius: 0"
```
This is our first taste of how larger programs are built: we define basic operations, then combine them in ever-large chunks to get the effect we want. Real-life functions will usually be larger than the ones shown here—typically half a dozen to a few dozen lines—but they shouldn’t ever be much longer than that, or the next person who reads it won’t be able to understand what’s going on. **Modular programming**

## Challenge 1
Goal : Wrapped function calls.
As we’ve seen in our print statements, we can use `paste` or `paste0` to concatenate strings.

- Write a function called `fence` that takes two parameters called `original` and `wrapper` and returns a new string that has the `wrapper` character at the beginning and end of the `original`.


Example function call and output:
```shell=
fence('name', '---')
---name---
```
**Solution**

```shell=
# function to surround a piece of text with other text
fence <- function(original, wrapper) {
  result <- paste0(wrapper, original, wrapper)
  
  return(result)
}

# test function call
print(fence('James', '***'))
```
```
## [1] "***James***"
```

## Explaining the R Environments

Lets write a new script for our gapminder dataset:
```shell=
# This script computes the average GDP for Albania using the gapminder data

# location of the data
fileName <- 'gapminder.txt'

# read the data file
gapminder <- read.table(fileName, header=TRUE)

# select the rows where the country is Albania and store it in albaniaData
albaniaData <- gapminder[gapminder$country == 'Albania',]

# select the column containing the GDP per capita from the Albania data
albaniaGdp <- albaniaData$gdpPercap

# compute the average GDP value
albaniaAverageGdp <- mean(albaniaGdp)

# print a message with the result of our computation
print(paste('The average GDP of Albania is', albaniaAverageGdp))
```
```
## [1] "The average GDP of Albania is 3255.36663266667"
```
Now make a small change:
```shell=
# This script computes the average GDP for Albania using the gapminder data

# location of the data
fileName <- 'gapminder.txt'

# read the data file
gapminder <- read.table(fileName, header=TRUE)

# create a variable to store a country name
countryName <- 'Albania'

# select the rows where the country is countryName and store it in albaniaData
albaniaData <- gapminder[gapminder$country == countryName,]     # note the change here

# select the column containing the GDP per capita from the Albania data
albaniaGdp <- albaniaData$gdpPercap

# compute the average GDP value
albaniaAverageGdp <- mean(albaniaGdp)

# print a message with the result of our computation
print(paste('The average GDP of', countryName, 'is', albaniaAverageGdp)) # and the change here
```
```
## [1] "The average GDP of Albania is 3255.36663266667"
```
Would using country instead of countryName cause any conflict with gapminder$country? No.


In a new script file, write a function `getAverageGdpPerCapita` that takes the name of a country and the gapminder dataset as its two inputs, then computes the averaged GDP per capita and returns it.
```shell=
# This script computes the average GDP for a country using the gapminder data

# clear old variables
rm(list=ls())

# location of the data
fileName <- 'gapminder.txt'

# read the data file
gapminder <- read.csv(fileName)

getAverageGdpPerCapita <- function(country, gapminder) {
  # extract gdpPercap from the gapminder data for the specified country.
  
  selectedCountryData <- gapminder[gapminder$country == country, 'gdpPercap']
  
  mean(selectedCountryData)
}
```

Try out our new function
```shell=
gdpUSA <- getAverageGdpPerCapita('United States', gapminder)
gdpCanada <- getAverageGdpPerCapita('Canada', gapminder)
gdpMexico <- getAverageGdpPerCapita('Mexico', gapminder)
```

What will happen if we remove the second argument to the function? Will it throw an error?
```shell=
getAverageGdpPerCapita <- function(country) {
  # extract gdpPercap from the gapminder data for the specified country.
  
  selectedCountryData <- gapminder[gapminder$country == country, 'gdpPercap']
  
  mean(selectedCountryData)
}

gdpUSA <- getAverageGdpPerCapita('United States')
gdpCanada <- getAverageGdpPerCapita('Canada')
gdpMexico <- getAverageGdpPerCapita('Mexico')

print(paste('GDP of USA is', gdpUSA))
```
```
## [1] "GDP of USA is 26261.1513466667"
```
```shell=
print(paste('GDP of Canada is', gdpCanada))
```
```
## [1] "GDP of Canada is 22410.74634"
```
```shell=
print(paste('GDP of Mexico is', gdpMexico))
```
```
## [1] "GDP of Mexico is 7724.11267458333"
```
When we create new variables, they are created in the current frame, which is initially the global frame:
```
search()
```
```
##  [1] ".GlobalEnv"        "package:knitr"     "package:stats"    
##  [4] "package:graphics"  "package:grDevices" "package:utils"    
##  [7] "package:datasets"  "package:methods"   "Autoloads"        
## [10] "package:base"
```

When we access a variable, those variables are also searched for in the current frame.

When a function is called, R searches for variables that are arguments to the function and any new variables that are created in the function. If a variable cannot be found, it searched for in its parent frame. The parent frame is the frame where it is defined, and not where it is called.

## Defualt Values

Modify the function getAverageGdpPerCapita that accepts 3 arguments - a country name, a start year, and an end year. The function should compute the average gdp of that country between the range of years supplied. Use the logical `&` operator to combine the multiple conditions required. Or you can apply the three conditions one afer the other.
```shell=
getAverageGdpPerCapita <- function(country, startYear, endYear) {
  # extract gdpPercap from the gapminder data for the specified country.
  
  selectedCountryData <- gapminder[gapminder$country == country & 
                                     gapminder$year >= startYear & 
                                     gapminder$year <= endYear, 'gdpPercap']
  
  mean(selectedCountryData)
}

gdpUSA <- getAverageGdpPerCapita('United States', 1980, 1989)
gdpCanada <- getAverageGdpPerCapita('Canada')

print(paste('GDP of USA is', gdpUSA))
print(paste('GDP of Canada is', gdpCanada))
```
Let’s say that if start and end year are not specified, we want to default to a start year of 1952 and an end year of 2007.
```shell=
getAverageGdpPerCapita <- function(country, startYear = 1952, endYear = 2007) {
  # extract gdpPercap from the gapminder data for the specified country.
  
  selectedCountryData <- gapminder[gapminder$country == country & 
                                     gapminder$year >= startYear & 
                                     gapminder$year <= endYear, 'gdpPercap']
  
  mean(selectedCountryData)
}

gdpUSA <- getAverageGdpPerCapita('United States', 1980, 1989)
gdpCanada <- getAverageGdpPerCapita('Canada')

print(paste('GDP of USA is', gdpUSA))
```
```
## [1] "GDP of USA is 27446.954775"
```
```shell=
print(paste('GDP of Canada is', gdpCanada))
```
```
## [1] "GDP of Canada is 22410.74634"
```

Note the use of an = sign instead of the arrow `<-`.

Show the documentation of the read.csv function.
```shell=
read.csv(file, header = TRUE, sep = ",", quote = "\"",
         dec = ".", fill = TRUE, comment.char = "", ...)
```

That is why
```shell=
file <- 'myfile.csv'
read.csv(file)
```
works.

What if we switch the start and end years?
```shell=
gdpUSA <- getAverageGdpPerCapita('United States', 1989, 1980)
```
It won’t work, as R matches the arguments by position. But, we can specify arguments by name as
```shell=
gdpUSA <- getAverageGdpPerCapita('United States', endYear = 1989, startYear = 1980)
```
We can even say
```shell=
gdpUSA <- getAverageGdpPerCapita('United States', endYear = 1989)
```
in which case the start year will take on its default value.
## Processing large vectors using the `apply` functions
In our later sessions, we are going to see control statements like loops. One of their uses is to go through an array and do a task on its elements one by one. Without getting into loops, we will quickly demonstrate the <code>apply</code> family of functions which let us achieve something similar:
```shell=
southAmericanCountries <- c('Argentina', 'Bolivia', 'Brazil', 'Chile', 'Colombia', 'Ecuador', 'Paraguay', 'Peru', 'Uruguay', 'Venezuela')

# use sapply to invoke getAverageGdpPerCapita() on all elements of southAmericanCountries
averagedGdpSouthAmericanCountries <- sapply(southAmericanCountries, getAverageGdpPerCapita)

# sort them in ascending order
averagedGdpSouthAmericanCountries <- averagedGdpSouthAmericanCountries[order(averagedGdpSouthAmericanCountries)]

barplot(averagedGdpSouthAmericanCountries, las=2)
```
<p><img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABUAAAAPACAMAAADDuCPrAAADAFBMVEUAAAABAQECAgIDAwMEBAQFBQUGBgYHBwcICAgJCQkKCgoLCwsMDAwNDQ0ODg4PDw8QEBARERESEhITExMUFBQVFRUWFhYXFxcYGBgZGRkaGhobGxscHBwdHR0eHh4fHx8gICAhISEiIiIjIyMkJCQlJSUmJiYnJycoKCgpKSkqKiorKyssLCwtLS0uLi4vLy8wMDAxMTEyMjIzMzM0NDQ1NTU2NjY3Nzc4ODg5OTk6Ojo7Ozs8PDw9PT0+Pj4/Pz9AQEBBQUFCQkJDQ0NERERFRUVGRkZHR0dISEhJSUlKSkpLS0tMTExNTU1OTk5PT09QUFBRUVFSUlJTU1NUVFRVVVVWVlZXV1dYWFhZWVlaWlpbW1tcXFxdXV1eXl5fX19gYGBhYWFiYmJjY2NkZGRlZWVmZmZnZ2doaGhpaWlqampra2tsbGxtbW1ubm5vb29wcHBxcXFycnJzc3N0dHR1dXV2dnZ3d3d4eHh5eXl6enp7e3t8fHx9fX1+fn5/f3+AgICBgYGCgoKDg4OEhISFhYWGhoaHh4eIiIiJiYmKioqLi4uMjIyNjY2Ojo6Pj4+QkJCRkZGSkpKTk5OUlJSVlZWWlpaXl5eYmJiZmZmampqbm5ucnJydnZ2enp6fn5+goKChoaGioqKjo6OkpKSlpaWmpqanp6eoqKipqamqqqqrq6usrKytra2urq6vr6+wsLCxsbGysrKzs7O0tLS1tbW2tra3t7e4uLi5ubm6urq7u7u8vLy9vb2+vr6/v7/AwMDBwcHCwsLDw8PExMTFxcXGxsbHx8fIyMjJycnKysrLy8vMzMzNzc3Ozs7Pz8/Q0NDR0dHS0tLT09PU1NTV1dXW1tbX19fY2NjZ2dna2trb29vc3Nzd3d3e3t7f39/g4ODh4eHi4uLj4+Pk5OTl5eXm5ubn5+fo6Ojp6enq6urr6+vs7Ozt7e3u7u7v7+/w8PDx8fHy8vLz8/P09PT19fX29vb39/f4+Pj5+fn6+vr7+/v8/Pz9/f3+/v7////isF19AAAACXBIWXMAAB2HAAAdhwGP5fFlAAAgAElEQVR4nO3deYBU1Zmw8ZeloWlBRIhoRBRwA40LalziuKExDiaKRPwg7tG4oDGiuEQjE8WAaMQvmWhEo5loXJK4RDTMuMUlMRH9NKiJUUQygIorIm5sfb9ae6vSPv32ec+pqvv8/rCrTkOdavv2Q9Xte8+VBACgIrGfAABUKwIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACgREABQImAAoASAQUAJQIKAEoEFACUCCgAKBFQAFAioACg5BjQ2Td92OLe0ycMq19/5+nLOjsCANXMLaBvdpPFzfcu7So5g5/u3AgAVDW3gP5YWgT0mkwFD5oyaTORgYs7MwIA1c0poM81tAjo0l7SfXbm48rDRSZ0YgQAqly7AW1cNOfb9dIioOeJnJ+7sWKQdF2gHwGAKtduQA/K77lsCmjj5iLz8zfPFpmpHgGQNit+eK6JKctjfUXtBnRUm4C+IjK8cPNRkQPVIwDS5mYxckOsr6jdgL7/dsa+zQG9W+SMws3VDTJIPQIgbW6QrU40MFx+Husrcvst/IHNAZ0h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" title="" alt="" width="672"></p>


## Key Points
- Define a function using `function` name(…params…)
- The body of a function should be indented.
- Call a function using name(…values…).
- Numbers are stored as integers or floating-point numbers.
- Each time a function is called, a new stack frame is created on the call stack to hold its parameters and local variables.
- R looks for variables in the current environment before looking for them at the top level.
- Use help(thing) to view help for something.
- Put docstrings in functions to provide help for that function.
- Annotate your code!
- Specify default values for parameters when defining a function using name=value in the parameter list.
- Parameters can be passed by matching based on name, by position, or by omitting them (in which case the default value is used).



# Calling R scripts from the command line
Just like we can call other scripts and functions from our R programs, we can call an R script from the command line. We use the Rscript program to do this.

`Rscript filename.R`

If Rscript is not on your system’s path, you can invoke Rscript using it’s full path name.

Try it out:

script.R:

```shell=
print('This is a simple R script')
```
On the command line:

```shell=
Rscript script.R
```
Even if you do your data analysis in a different programming language, you can still use R’s plotting capabilities (which we will learn more about in the afternoon session). So if the majority of your work is in another programming language, you can still make use of R to do parts of the analysis, or only to make publication quality plots.

We will write a script that will produce a barplot from a given datafile. In the previous example, script.R prints a fixed message and has no way of getting any information from the shell. Rscript allows you to send arguments to the R script by specifying them after the file name:

```shell=
Rscript filename.R argument_1 argument_2 ...
```

These arguments can be accesed from within the R script by using the `commandArgs()` function. By default the list will include the name of the R executable, the script file name, and several switches. Using `commandArgs(FALSE)` only presents us with the arguments starting from `argument_1` onwards.

Updated script.R

```shell=
countryList <- commandArgs(TRUE)

# location of the data
fileName <- 'gapminder.txt'

# read gapminder data
gapminder <- read.csv(fileName)

getAverageGdpPerCapita <- function(country) {
  # extract gdpPercap from the gapminder data for the specified country.
  
  selectedCountryData <- gapminder[gapminder$country == country, 'gdpPercap']
  
  mean(selectedCountryData)
}

averagedGdp <- sapply(countryList, getAverageGdpPerCapita)
barplot(averagedGdp)

print(averagedGdp)
```

We now write a shell script that is going to call this method on a list of countries.

Create a file `makePlots.sh`

```shell=
countries="Canada Belgium"
Rscript cmdScript.R $countries
```

Run it from bash:

```shell=
bash makePlots.sh
```

The generated plots are saved in PDF format in the file `Rplots.pdf`.