# CSE 15L Week 5 Lab Report: Researching Commands (grep)

*Ian Venzon - Thursday 12:00 PM - B270*

## The grep command:

In this lab report, the command we will be taking a look at is `grep`. The `grep` command takes in a patten, then searches a file for the given pattern. It will then display all of the lines that contain said pattern. The syntax for `grep` is given by the following:

```
grep [options] pattern [files]
```

Source: [GeeksForGeeks: grep command in Unix/Linux](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)

However, there are alternative commands to `grep` that can give us similar results. This is what we will be exploring in this lab report.

## Alternative #1: The AWK command:

The `awk` command is another useful way we can search through files/directories for a specific pattern. The syntax for `awk` is more complicated than grep, but still uses the same general premise:

```
awk [options] 'pattern {action}' [input-file] > [output-file]
```
Source: [GeeksForGeeks: AWK command in Unix/Linux](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)

With `awk`, we can actually specify what action we want to do. To achieve a similar result as `grep`, we should use the `print` action. For instance, if we wanted to search for all of the .txt files within `./written_2` (where `find-results.txt` contains all of the files/directories within `./written_2`) that contain the word "Italy", we could use `awk` in the following way:

```
awk '/Italy/ {print}' find-results.txt
```
![Image](https://i.imgur.com/XLnIiPn.png)

`awk` can also be used to search for specific words/phrases within a .txt file. If we wanted to search for all the lines within the `./written_2/travel_guides/berlitz1/` directory that contain the word "vista", we would use `awk` as such:

```
awk '/vista/ {print}' written_2/travel_guides/berlitz1/*.txt
```
![Image](https://i.imgur.com/jDmmPZQ.png)

From our search with `awk`, we can see that there are 16 lines within the `/berlitz1/` directory that contain "vista".

## Alternative #2: The Sed command:

The `sed` command in Linux stands for "stream editor" and can be used in a manner similar to `grep`. However, it can be used in more specialized ways than `grep`, which gives it an edge in certian use cases. The syntax for `sed` is as follows:

```
sed [options]... [script] [input-file...]
```
Source: [GeeksForGeeks: Sed command in Unix/Linux](https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/)

For example, what if I wanted to search for lines 5-10 of a given file (in this case, `find-results.txt`. I'd have no real way to approach this with `grep`, but with `sed`, it's as easy as the following:

```
sed -n 5,10p find-results.txt
```
![Image](https://i.imgur.com/UbUDLoz.png)

To explain, the `-n` option suppresses the default output behavior of `sed` and makes it so only explicit print statements will go through. Then, the `5,10p` portion states which lines to print, being 5-10. (Source/Idea: [Linux Commando: Using sed to extract lines in a text file](https://linuxcommando.blogspot.com/2008/03/using-sed-to-extract-lines-in-text-file.html))


