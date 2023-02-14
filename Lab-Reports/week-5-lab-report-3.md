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
