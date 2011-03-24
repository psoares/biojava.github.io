---
title: Short coding exercise
---

**Goal 1:**

Implement the interface

` public interface StringOverlapFinder {`  
`     String getOverlap(String x, String y);`  
` }`

The getOverlap function should locate the overlap of the end of x with
the beginning of y.  
The function should return the non-overlapping start of x If x does not
match the first length(x) characters of y, then return x. The minimum
overlap should be 5 or more characters.

**Goal 2:**

The function should be wrapped up to accept a file, from the command
line, that has two columns.

The resulting program should accept the file, feeding the function with
each element from the column and print the result to either an out file
or a standard output.

Example Command:

`  java FindEnds inputFile.txt outputFile.txt`

**Goal 3:**

Code under the assumption that

-   The input file does not fit into memory
-   The length of the individual strings to compare can be up to 100000
    characters (fits into memory).

**Example of Function Input and Result:**

x = "abcdefghijklm"

y = "hijklmnopqrst"

return: "abcdefg"

**Example Input File:**

`   Column_1 (x) Column_2 (y)`  
`   abcdefghijklm hijklmnopqrstuvw`  
`   aioludhfgakjn akjnopqrstuvwxuh`  
`   ......        .......`  
`   ......        .......`

There will be no header in the file and the columns are separated with a
tab character (\\t).

**Target:**

The target is optimal code, therefore there are several goals (in no
particular order):

-   Code quality (maintability, reusability, OO design, etc)
-   CPU & RAM efficiency

Using multiple threads to speed up the comparison is a plus.

**Please note that the task is not very well defined** and you will have
to make some assumptions, please make sure to document all of them. Also
provide an appropriate Javadoc for your program if you coding for the
goal 2 or 3.

Either code for one, two or all of the goals.