---
title: "Morgado Assignment"
author: "Rod Morgado"
date: "7/5/2021"
output: pdf_document
---

## This is a markdown file 


## Summary

Data Types

* Atomic classes: numeric, logical, character, integer, complex
* Vectors, lists
* Factors
* Missing Values
* Data Frames
* Names

## Reading Data

* read.table, read.csv, for reading tabular data.
* readLines, for reading lines of a text file.
* source, for radin in R code files (inverse dump).
* dget, for reading in R code files (inverse of dput).
* load, for reading in saved workspaces.
* unserialize, for reading single R objects in binary form.

## Writing Data

* write.table
* writeLines
* dump
* dput
* save
* serialize

## Reading Data Files with read.table

* file, the name of the file, or a connection.
* header, logical indicating if the file has a header line.
* sep, a string indicating how the columns are separated.
* colClasses, a character vector indicating the class of each column in the dataset.
* nrows, the number of rows in the dataset.
* comment.char, a character string indicating the comment character.
* skip, the number of lines to skip from the beginning.
* stringAsFactors, should character variables be coded as factors?.

### read.table

`data <- read.table("foo.txt")`

R will automatically
* skip lines that begin with a #
* figure out how many rows there are
* figure what type of variables is in each column of the table Telling R all these thingss directly makes R run faster and more efficiently.
* read.csv does the same, but it's separated by commas.

## Reading Large Tables with read.table

With much larger datasets, doing the following things will make your life eassier and will prevent R from choking.

* Read the help page for read.table, which contains many hints.
* Make a rough calculation of the memory required to store your dataset. If the dataset is larger than the amount of RAM on your computer you can probably stop there.

* Use the colClasses argument. Specifying this option instead of using the default can make 'read.table' run much faster, often twice as fast.

`initial <- read.table("datatable.text", nrows = 100)`
`classes <- sapply(initial, class)`
`tabAll <- read.table("datatable.txt, colClasses = classes)`

* Set nrows. This doesn't make R run faster, but it helps with memory usage. A mild overestimate is okay. You can use the Unix tool wx to calculate the number of lines in a file.

## Know Thy System

In general:

* How much memory is available?
* What other applications are in use?
* Are there other users logged into the same system?
* What about th OS?
* Is the OS 32 or 64 bits?

## Calculating Memory Requirements

I have a data frame with 1,500,000 rows and 120 columns, all of which are numeric data. Roughly, how much memory is required to store this data frame?

1,500,000 x 120 x 8 bytes/numeric
= 144000000000 bytes
= 144000000000 / 2^20 bytes/Mb
= 1,373.29 MB
= 1,34 GB

You almost need twice of this memory available.

## Textual Formats

* dumping and dputing are useful because the resulting textual format is edit-able, and in the case of corruption, potentially recoverable.

`y <- data.frame(a = 1, b = "a")`
`dput(y)`
`structure(list(a = 1), b = sructure(1L, .Label = "a", class = "factr")), .Names = c("a", "b"), row.names = c(NA, -1L), class = "data.frame")`
`dput(y, file = "y.R")`
`new.y <- dget(y.R)`
`new.y`
  a  b
1 1  a

## Interfaces to the outside world

Data are read in using connection interfaces. Connections can be made to fils (most common) or to other more exotic things.

* file, opens a connection to a file
* gzfile, opens a connectino to a file compressed with gzip

`con <- file("foo.txt", "r")`
`data <- read.csv(con)`
`close(con)`

is the same that

`data <- read.csv("foo.txt")`

This might take time

`con <- url("http://")`

## Subsetting - Basics

There are a number of operators that can be used to extract subsets of R objects

* [ always returns an object of the same class as th eoriginal; can be used to select mor than one element (there is one exception)

## Repeat

The loop in the previous slide is a bit dangerous because there's no guarantee it will stop. Better to set a hard limit on the number of iterations.

## Control Structures

Summary
* Control structures like if, while, and for allow you to control the flow of the R program.
* Infinite loops shold generally be avoided, even if they are theorically correct.

## Some Recommendations

* Indenting improves readbility
* Always use a text editor
* Limit the width of your code (80 columns?)
* Limit the length of individual functions

## Dates and Times in R

R has developed a special representationo of dates and times

* Dates are represented by the Date Class
* Times are represented by the POSIXct of the POSIXlt class
* Dates are stored interrnally as the number of dayss since 1970

Times in Re

Times are represented using the POSIXct and PSIXcl