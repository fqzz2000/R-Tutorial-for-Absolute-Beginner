Quick R tutorial for STATS101
=============================

#### Quanzhi Fu

#### Nov.3 2022

This is a quick tutorial of R, for those students who have little background in computer science or programming. In this document, I will explain some basic concepts of programming and some useful techniques in R (in a hopefully systematical way). Most of them are comes from questions from your classmate. I will provide plenty of examples and explanations about each command. Hope this document will help you better prepare for this course’s study~

Plese let me know if you have any suggestions or questions about this tutorials.

This document is written in R markdown. R markdown is a tool that can embed R code and R result into the a notebook. It is a useful tool for statistical analysis and it is also a good way for you to deliver your homework.You can create your own R markdown file by clicking File->New File->R Markdown in RStudio.

Variables
---------

Varibales are one of the basic components for most programming languages, including R. Intuitively, you can think variables as a “named box” in order to store your data. Varibales provides a easy way for you store and refer to lot of different datas.

In R, you can create a variable with all English characters, numbers, dot(.) and underline(\_) to create a variable (but only the English character can be used as the first character of a variable name), and assign a value to a variable using “<-” operator (“=” has the similar effect but they have some subtle difference). Whenever you declare a variable, you must assign a value to it (refer to an empty box make no sense!).

You can refer to a variable by directly call its name. print is a function used to display the value to the screen. We will talk about function later.

    # the after "#" is called comment, this will not be considered as command by R
    
    a <- 5 # assign 5 to a (reate a "box" called v and store 5 into it)
    
    print(a) # now a just refers to 5
    
    ## [1] 5

After you assign a value to a variable. You can use this variable to do any computation just as you are using the original value. You can also assign the result for some computation for to a new value.

    a <- 2 # assign 5 to a
    
    b <- 10.5 # assign 10.5 to b
    
    c <- a * b # assign the result of a * b to c
    
    print(c) # c is just 21, the effect of c <- a * b is same as c <- 2 * 10.5
    
    ## [1] 21

You can also assign text to a variable. Text in programming has another name: string. It was called string as text in computer is just a sequence characters ordered like a string.

    a <- "Hello"
    
    b <- "World"
    
    cat(a, b) # cat is a function that caoncatenate two strings together we will talk about function later
    
    ## Hello World

Variables are powerful. It asks the computer to remember some important result and allows you to do some super complicated computation.

Functions
---------

Functions is also a key concept in programming language. Function in programming is similar to the function concept in mathematics. It takes some values (called `arguments` or `parameters` in programming) and provide you a new value (called `return value` in programming) based on the value it taken. For example, in mathematics you can define a square root function.

\\\[ f(x) = \\sqrt{x} \\\]

If you put 4 into this function, you will get 2, because 2 is the square root of 4.

\\\[ f(4) = 2 \\\]

In R, you can use function just like in math, by putting a paranthesis `()` after the function name and putting your arguments inside the parathesis. (do not confused `()` with `[]`, `[]` is a special operator used to access data in data frame/vector, and `()` used for functions) For example, if you want to compute the square root of 4 in R. You can use

    sqrt(4)
    
    ## [1] 2

`sqrt` is a build in function (build-in means have been wrote for you) in R used to compute the square root. In this function, the argument passed to the function is 4, and the return value from the function is 2. Because we didn’t hold the return value, so the return value simply display on the screen and discarded by the R.

You can also save the return value into a variable in the exactly same way as you save other values into a variable. In the following example, we assign the result of `sqrt(4)` to variable `v`. Because we pass the value to a variable, nothing will be displayed on the screen.

    var <- sqrt(4)

### function arguments

Functions take arguments. In R all arguments have its name. Take the `print` function as an example. if you type `help(print)` in your R console, a help page will pop up and show you the arguments of print. The first argument of print is called `x`, which is the value you want print out. You can use a `=` operator in function parenthesis to set value for this arguments.

    print(x = "Hello World") # assign x = Hello World
    
    ## [1] "Hello World"

Most of build-in functions takes a lot of arguments. Fortunately, you do not need to remember all of them. Most of these arguments are optional, which means you do not need to pass their value unless you really have a reason to do so. Also, you can ignore the argument name and the `=` operator as long as you are pass the argument in the correct order.

    print("Hello World") # x is the first argument so we can directly put "Hello World" here
    
    ## [1] "Hello World"

Another example is about function `mean`, which compute the mean value of your data. The first argument name is also `x` (check `help(mean)`). So you can call `mean` function in these two equivalent ways.

    mean(x = 1:5) # recall that 1:5 just means 1, 2, 3, 4, 5
    
    ## [1] 3
    
    mean(1:5)
    
    ## [1] 3

If you want to change a value for a specific argument, you need to include their name. For example, you may want the mean function ignore `NA` during the computation.

    mean(1:5, na.rm = T)
    
    ## [1] 3
    
    mean.value <- mean(1:5, na.rm = T) # similarly you can assign the result to a variable

### declare your own functions

R provides a lot of commonly used functions like `mean`, `median`, `IQR` etc. Besides using these functions, you can build your own function. The syntax to delare your own function is like this.

    myFunction <- function(arg1, arg2) {
      ans = arg1 + arg2
      return (ans)
    }

The above code declared a function called `myFunction` with two required arguments `arg1` and `arg2`. By executing this function, you can get the result of the sum of them. After declare your own function, you can use it just like build in functions.

    myFunction(3, 5) # return 3 + 5 = 8
    
    ## [1] 8

Data Types
----------

We have seen the basic usage of variables. However, data in real world data is not just simple integers or strings. Data are complicated table that mix with string, integer, float etc. Think about how annoying it would be if you try to assign each value to a variable from a Excel table.

Fortunately, R provides a lot of different data types other than simple integer and string. to help deal with the complicated data. The most frequently used two data types in our courses are

*   Vectors
*   Data Frames

### Vector

#### Vector Generation

Vector is one of the most commonly used data type in R programming. Vector is simple a sequence of data together. You can create a vector use function c(). c is stands for “concatenate”, it will concatenate multiple data/variables together and make a vector.

    v0 <- c(1, 3, 5, 7) # create a vector with content 1, 3, 5, 7
    v1 <- c(2, 4, 6) # create another vector with content 2, 4, 6
    v2 <- c(v0, -1, v1, -2) # you can concat vectors with different length together, or even concat vector with numbers
    print(v2)
    
    ## [1]  1  3  5  7 -1  2  4  6 -2

R provide some simple ways to generate vectors. Some most frequently used are seq(), rep(), and “:”. The easiest way to generate a continuous vector is to use “:” operator.

    print(3:9) # this basically generate 3, 4, 5, 6, 7, 8, 9
    
    ## [1] 3 4 5 6 7 8 9
    
    v <- 3:9 # you can assign the result to a vector
    print(v) 
    
    ## [1] 3 4 5 6 7 8 9

The second way to genetrate a vertor is to use seq(), seq is used to generate a sequence and have three arguments: `from`, `to` and `by`. `from` denotes the start, `to` denotes the upper bound of your sequence and `by` denotes the stpe size.

    seq0 <- seq(from=0, to=10, by=1) #same as 0:10
    print(seq0)
    
    ##  [1]  0  1  2  3  4  5  6  7  8  9 10
    
    seq1 <- seq(from=0, to=9, by=2) 
    print(seq1) # note that seq may not reach "to" which is 9 in this senario as 9 can not be express as 0 + 2 * N
    
    ## [1] 0 2 4 6 8

The last way to generate a vector is to use rep(), rep stands for “repeat”, it could repeat the input multiple times. It can repeat a single value, or a whole vector. The rep() function has a argument called `each`, which can repeat each element in the provided vectors multiple times.

    v0 <- rep(10, 3) # repeat 10 3 times
    print(v0)
    
    ## [1] 10 10 10
    
    v1 <- rep(1:5, 5) # repeat vector 1:5 5 times
    print(v1)
    
    ##  [1] 1 2 3 4 5 1 2 3 4 5 1 2 3 4 5 1 2 3 4 5 1 2 3 4 5
    
    v2 <- rep(1:5, each = 5) # repeat each element in 1:5 5 times
    print(v2)
    
    ##  [1] 1 1 1 1 1 2 2 2 2 2 3 3 3 3 3 4 4 4 4 4 5 5 5 5 5

You can access the data in Vector using `[]` operator.

    v1 <- 1:10
    v1[2] # access the second element in v1
    
    ## [1] 2

#### Vectorized Operation

R provides many operations for vectors. Familiar with these operations will make your analyze much easier.

You can do arithmetics and comparisons (add +, minus -, times \*, divide /, and &, or |, greater than >, smaller than <, equal ==, not equal !=, greater than or equals to >=, smaller than or equals to <=) between same length vectors and between vectors and single value.

    a <- 1:5
    b <- 2:6
    a + b
    
    ## [1]  3  5  7  9 11
    
    a * b
    
    ## [1]  2  6 12 20 30
    
    a / b
    
    ## [1] 0.5000000 0.6666667 0.7500000 0.8000000 0.8333333
    
    a - b
    
    ## [1] -1 -1 -1 -1 -1
    
    b == 5
    
    ## [1] FALSE FALSE FALSE  TRUE FALSE
    
    a > 3
    
    ## [1] FALSE FALSE FALSE  TRUE  TRUE
    
    b > 3
    
    ## [1] FALSE FALSE  TRUE  TRUE  TRUE
    
    a > 3 & b > 3
    
    ## [1] FALSE FALSE FALSE  TRUE  TRUE

Note that there are two other operators logical and (&&) and logical (||), these two operators cannot be used to perform element-wised and and or.

### Data Frames

Data Frames is the R data strcuture which is very similar to an Excel table. It provide each row a index, and a name for each columns. Here we use CO2 a build-in data frame (build-in dataset means R has already assign the correct value to its name, you can refer to this dataset by directly call CO2) in R which records carbon dioxide uptake in grass plants. Here is how this dataframe looks like. In the rest of this section, I will show you some frequently used way to playing with Data Frame.

    head(CO2, 10) # extract the top 10 line of CO2
    
    ##    Plant   Type  Treatment conc uptake
    ## 1    Qn1 Quebec nonchilled   95   16.0
    ## 2    Qn1 Quebec nonchilled  175   30.4
    ## 3    Qn1 Quebec nonchilled  250   34.8
    ## 4    Qn1 Quebec nonchilled  350   37.2
    ## 5    Qn1 Quebec nonchilled  500   35.3
    ## 6    Qn1 Quebec nonchilled  675   39.2
    ## 7    Qn1 Quebec nonchilled 1000   39.7
    ## 8    Qn2 Quebec nonchilled   95   13.6
    ## 9    Qn2 Quebec nonchilled  175   27.3
    ## 10   Qn2 Quebec nonchilled  250   37.1

For a Data Frame, you can access data in it use “\[\]”. For example, if you want to access the first 5 rows of this Data Set. You can use CO2\[1:5,\]. Note that there is a comma inside the \[\] because there are two-dimensions of a data frame, we put 1:5 before the comma indictae that we choose the rows instead of columns. Type nothing after the comma means that we want all columns.

    CO2[6, ] # select 6th row
    
    ##   Plant   Type  Treatment conc uptake
    ## 6   Qn1 Quebec nonchilled  675   39.2
    
    CO2[1:5,]# select rows 1:5
    
    ##   Plant   Type  Treatment conc uptake
    ## 1   Qn1 Quebec nonchilled   95   16.0
    ## 2   Qn1 Quebec nonchilled  175   30.4
    ## 3   Qn1 Quebec nonchilled  250   34.8
    ## 4   Qn1 Quebec nonchilled  350   37.2
    ## 5   Qn1 Quebec nonchilled  500   35.3
    
    CO2[5:1,]
    
    ##   Plant   Type  Treatment conc uptake
    ## 5   Qn1 Quebec nonchilled  500   35.3
    ## 4   Qn1 Quebec nonchilled  350   37.2
    ## 3   Qn1 Quebec nonchilled  250   34.8
    ## 2   Qn1 Quebec nonchilled  175   30.4
    ## 1   Qn1 Quebec nonchilled   95   16.0

note that the order matters when we select rows or columns, CO2\[1:5, \] and CO2\[5:1, \] display the first five row in opposite direction. (this is how `order()` works which you have used in homework 1)

Similarly, you can access column by type numbers after comma

    CO2[1:5, c(1, 3)] # select first five rows of columns 1 and 3
    
    ##   Plant  Treatment
    ## 1   Qn1 nonchilled
    ## 2   Qn1 nonchilled
    ## 3   Qn1 nonchilled
    ## 4   Qn1 nonchilled
    ## 5   Qn1 nonchilled
    
    CO2[1:5, 5]       # select first five rows of the 3th column 
    
    ## [1] 16.0 30.4 34.8 37.2 35.3

You can also access data in data through column names or use `$` sign

    CO2[1:5, "uptake"];
    
    ## [1] 16.0 30.4 34.8 37.2 35.3
    
    CO2[1:5, c("Plant", "uptake")]
    
    ##   Plant uptake
    ## 1   Qn1   16.0
    ## 2   Qn1   30.4
    ## 3   Qn1   34.8
    ## 4   Qn1   37.2
    ## 5   Qn1   35.3
    
    CO2$uptake[1:5] # select first five rows of update data
    
    ## [1] 16.0 30.4 34.8 37.2 35.3
    
    CO2[1:5,]$uptake # you can also select column name based on a subarrary
    
    ## [1] 16.0 30.4 34.8 37.2 35.3

By using `[]` operator, R generate a temporary subset of the original data. Use `[]` on data frame will not change the value of original data. Similar to function, you can assign the temporary subset to a variable.

Besides directly select data based on index. Another commonly used way is based on boolean vectors. Boolean value, in computer science, means value that can only be `TRUE` and `FALSE`. When we select data based on boolean vectors, only rows with `TRUE` will be selected.

    a <- 1:5
    bool <- c(TRUE, TRUE, FALSE, FALSE, TRUE)
    a[bool]
    
    ## [1] 1 2 5

This feature enables us to do advanced search and filters in data frame. You can select the rows with `uptake` > 40 from our dataset.

    CO2[CO2$uptake > 40, ] # recall that CO2$uptake > 40 is just a boolean vector
    
    ##    Plant   Type  Treatment conc uptake
    ## 11   Qn2 Quebec nonchilled  350   41.8
    ## 12   Qn2 Quebec nonchilled  500   40.6
    ## 13   Qn2 Quebec nonchilled  675   41.4
    ## 14   Qn2 Quebec nonchilled 1000   44.3
    ## 17   Qn3 Quebec nonchilled  250   40.3
    ## 18   Qn3 Quebec nonchilled  350   42.1
    ## 19   Qn3 Quebec nonchilled  500   42.9
    ## 20   Qn3 Quebec nonchilled  675   43.9
    ## 21   Qn3 Quebec nonchilled 1000   45.5
    ## 35   Qc2 Quebec    chilled 1000   42.4
    ## 42   Qc3 Quebec    chilled 1000   41.4
    
    CO2[CO2$uptake > 40 & CO2$conc < 1000, ] # filter by multiple conditions
    
    ##    Plant   Type  Treatment conc uptake
    ## 11   Qn2 Quebec nonchilled  350   41.8
    ## 12   Qn2 Quebec nonchilled  500   40.6
    ## 13   Qn2 Quebec nonchilled  675   41.4
    ## 17   Qn3 Quebec nonchilled  250   40.3
    ## 18   Qn3 Quebec nonchilled  350   42.1
    ## 19   Qn3 Quebec nonchilled  500   42.9
    ## 20   Qn3 Quebec nonchilled  675   43.9
    
    CO2[CO2$uptake < 40 & CO2$uptake > 35, ] # you can even select a range of data
    
    ##    Plant        Type  Treatment conc uptake
    ## 4    Qn1      Quebec nonchilled  350   37.2
    ## 5    Qn1      Quebec nonchilled  500   35.3
    ## 6    Qn1      Quebec nonchilled  675   39.2
    ## 7    Qn1      Quebec nonchilled 1000   39.7
    ## 10   Qn2      Quebec nonchilled  250   37.1
    ## 27   Qc1      Quebec    chilled  675   35.4
    ## 28   Qc1      Quebec    chilled 1000   38.7
    ## 32   Qc2      Quebec    chilled  350   38.8
    ## 33   Qc2      Quebec    chilled  500   38.6
    ## 34   Qc2      Quebec    chilled  675   37.5
    ## 38   Qc3      Quebec    chilled  250   38.1
    ## 40   Qc3      Quebec    chilled  500   38.9
    ## 41   Qc3      Quebec    chilled  675   39.6
    ## 49   Mn1 Mississippi nonchilled 1000   35.5

Besides simply access data, you can assign value to data inside data frames based on the conditions and `[]` operator. We will use another build-in dataset women to illustrate this operation. `women` is a samll data frame that records height and weight of 15 women.

    women
    
    ##    height weight
    ## 1      58    115
    ## 2      59    117
    ## 3      60    120
    ## 4      61    123
    ## 5      62    126
    ## 6      63    129
    ## 7      64    132
    ## 8      65    135
    ## 9      66    139
    ## 10     67    142
    ## 11     68    146
    ## 12     69    150
    ## 13     70    154
    ## 14     71    159
    ## 15     72    164

using `[]` we can reassign value to the data

    women[women$height < 65,] = 42 # set all women whose height lower than 65 to 42
    women
    
    ##    height weight
    ## 1      42     42
    ## 2      42     42
    ## 3      42     42
    ## 4      42     42
    ## 5      42     42
    ## 6      42     42
    ## 7      42     42
    ## 8      65    135
    ## 9      66    139
    ## 10     67    142
    ## 11     68    146
    ## 12     69    150
    ## 13     70    154
    ## 14     71    159
    ## 15     72    164
    
    women[1:5,]$height = 1:5 # set the first five height into 1 2 3 4 5
    women
    
    ##    height weight
    ## 1       1     42
    ## 2       2     42
    ## 3       3     42
    ## 4       4     42
    ## 5       5     42
    ## 6      42     42
    ## 7      42     42
    ## 8      65    135
    ## 9      66    139
    ## 10     67    142
    ## 11     68    146
    ## 12     69    150
    ## 13     70    154
    ## 14     71    159
    ## 15     72    164

Besides these basic data access and assignment techniques with `[]` and conditions. There are two useful functions that are super useful when you dealing with data frames, which are `apply()` and `by()`.

#### apply()

apply function could apply a function to each row or each column of the data frame and return the reuslt as a vector. `apply()` takes 3 required arguments. `X`, `MARGIN`, and `FUN`. `X` is the data you are going to compute, `MARGIN` is indicate you are going to apply function on which dimension. `MARGIN = 1` means apply on each row, `MARGIN = 2` means apply on each column. `FUN` is the function you are going to apply. For example, if you want to compute the mean of each column in data frame women, you can use

    apply(women, 2, mean) # MARGIN = 2 because we want column mean
    
    ##   height   weight 
    ##  65.0000 136.7333

Use apply together with your self-defined function, you can did a lot of complicated task. For example, suppose you want to compute BMI (Body Mass Index) for the records in women dataset. You can first define a function that compute BMI and apply it to the whole dataset. Note that the function be applied to the data should only have one required argument.

    BMI <- function(record) {
      #convert height in inch to meter
      height = record[1] * 0.0254
      # convert weight in pounds to kilograms 
      weight = record[2] * 0.4536
      # equation : weight / height ** 2
      return (weight / height ** 2)
    }
    women$BMI <- apply(women, 1, BMI) # Margin = 1 because we want row mean 
    women
    
    ##    height weight      BMI
    ## 1      58    115 24.03518
    ## 2      59    117 23.63129
    ## 3      60    120 23.43605
    ## 4      61    123 23.24080
    ## 5      62    126 23.04585
    ## 6      63    129 22.85147
    ## 7      64    132 22.65790
    ## 8      65    135 22.46532
    ## 9      66    139 22.43533
    ## 10     67    142 22.24049
    ## 11     68    146 22.19937
    ## 12     69    150 22.15127
    ## 13     70    154 22.09684
    ## 14     71    159 22.17614
    ## 15     72    164 22.24254

#### by()

`by()` is another useful function. by stands for groupby, you may heard about this name if you have some experience with database. `by()` can group data based on the given groups and apply function for each of them. `by()` take three arguments, `data`, `INDICES`, `FUN`. `INDICES` indicate the function that how will we group the data. Use our data of homework 1 as a example. Suppose we want to compute the mean state’s turnout in each region. You can simply use

    setwd("../hw1")
    data <- read.csv("hw1.csv", na.strings =  c("","NA"))
    by(data$turnout, data$region, mean)
    
    ## data$region: Midwest
    ## [1] 56.50833
    ## -------------------------------------------------------- 
    ## data$region: Mountain West
    ## [1] 51
    ## -------------------------------------------------------- 
    ## data$region: Northeast
    ## [1] 53.5
    ## -------------------------------------------------------- 
    ## data$region: Pacific
    ## [1] 50.94
    ## -------------------------------------------------------- 
    ## data$region: South
    ## [1] 43.8875

You can also use it to compute the IQR for each regions adnum in one line

    by(data$adnum, data$region, IQR)
    
    ## data$region: Midwest
    ## [1] 2162155
    ## -------------------------------------------------------- 
    ## data$region: Mountain West
    ## [1] 1064550
    ## -------------------------------------------------------- 
    ## data$region: Northeast
    ## [1] 3691700
    ## -------------------------------------------------------- 
    ## data$region: Pacific
    ## [1] 1440679
    ## -------------------------------------------------------- 
    ## data$region: South
    ## [1] 1238976

Control Flow
------------

By default, your R command will be executed from the begin of your script to the end. Each line of the code will be executed exactly once. However, sometimes we do not want our programs work like this. We may want to execute some command multiple times (think about you are going to run a simulation for 1000 times), or we may want omit some instructions (if there are no NA in data, we can skip our command for processing NA). We can tell R to do it by us through “Control Flow”.Control Flow means that we are going to control the execution “flow” of our code.

There are two basic components of Control Flow - Conditional Statements (if, elseif, else) - Loop (for, while, repeat)

### Conditional Statements

Conditional statements will check the provided condition and decide if it will execute the command. The conditional statements in R are `if`, `else if`, `else`.

`if` is the most commonly used conditional statement in R and all programming languages. If statement will first evaluate the conditon in the parenthesis after it, if the condition is TRUE, command in its block will be executed, else the command in the block will be ignored. Here is a example of `if`

    x <- 10
    if (x < 15) {
      print("x is smaller than 15")
    }
    
    ## [1] "x is smaller than 15"
    
    if (x > 5) {
      print("x is larger than 5")
    }
    
    ## [1] "x is larger than 5"
    
    if (x < 5) {
      print("x is smaller than 5")
    }

You can use `if` with `else if` and `else` to create complicated control.

`else if` can only be used after `if`, and `else` can only be used after `if` and `else if`.

    x <- 15
    if (x < 10) {
      print("x is smaller than 10")
    } else if (x < 15) {
      print("x is between 10 and 15")
    } else {
      print("x is greater than or equals to 15")
    }
    
    ## [1] "x is greater than or equals to 15"

### Loop

Loop is another important component control flow. Think about if you are going to run a simulation for 1000 times. You don’t want to copy and paste your code for 1000 times. We can ask program to do the repeat works for us using loop. There are three types of loop in R: - for loop - while loop - repeat loop

We will mainly talk about for and while loops in R #### For loop For loop is the most commonly used loop in R. It could repeat the instructions in its block by a specific number of times. The basic syntax for for loop is like this

    for (i in 1:10) {
      print(i)
    }
    
    ## [1] 1
    ## [1] 2
    ## [1] 3
    ## [1] 4
    ## [1] 5
    ## [1] 6
    ## [1] 7
    ## [1] 8
    ## [1] 9
    ## [1] 10

You must write command that you want to be execute in loop between the `{}`. i is the loop varible used to record the iteration, you can call it whatever name you like, but by convention, people use i as the iteration variable.The i begin as 1 and in each iteration, it will update the value of i. The above block print the value of i in each iteration.

You can loop through some other vectors that designed by you.

    for (i in seq(1, 10, 2)) {
      print(i)
    }
    
    ## [1] 1
    ## [1] 3
    ## [1] 5
    ## [1] 7
    ## [1] 9

or

    words <- c("Hello", "World", "Hello", "Stats", "101")
    for (i in words) {
      print(i)
    }
    
    ## [1] "Hello"
    ## [1] "World"
    ## [1] "Hello"
    ## [1] "Stats"
    ## [1] "101"

#### While loop

The second type of loop is while loop. Different with for loop that you specifically set a vector to be looped through. While loop will keep loop until certain conditions are met. The basic syntax for while loop looks like this

    a = 0
    while (a <= 100) { # if the condition is TRUE, keep loop, else stop
      a = a + 3 # statement we execute 
    }
    a
    
    ## [1] 102

The above code will find the smallest multiple of three that greater than 100. After each iteration, the while loop will check if the condition `a <= 100` still hold. If `a <= 100` is TRUE, the loop will continue, otherwise it will stop. #### Control Your Loop You can use `break` or `next` to control the execution of your loop. Once a `break` executed in a loop. It will unconditionally end the loop. `next` will directly start a new iteration of the loop, omit the unexecuted command in the loop block.

    a = 0
    b = 0
    for (i in 1:10) {
      if (i == 5) {
        break
      }
      a = a + 1
      next
      b = b + 1
      
    }
    print(a)
    
    ## [1] 4
    
    print(b)
    
    ## [1] 0

The above example shows that how `next` will omit the unexecuted command in the loop block. `b = b + 1` did not be not executed. And rhe for loop is early stoped because when `i == 5` break command is executed.

loops can also be nested together, the following program print all combinations of digits from 0 to 3

    for (i in 0:3) {
      for (j in 0:3) {
        print(c(i, j))
      }
    }
    
    ## [1] 0 0
    ## [1] 0 1
    ## [1] 0 2
    ## [1] 0 3
    ## [1] 1 0
    ## [1] 1 1
    ## [1] 1 2
    ## [1] 1 3
    ## [1] 2 0
    ## [1] 2 1
    ## [1] 2 2
    ## [1] 2 3
    ## [1] 3 0
    ## [1] 3 1
    ## [1] 3 2
    ## [1] 3 3

R Markdown
----------

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see [http://rmarkdown.rstudio.com](http://rmarkdown.rstudio.com).
