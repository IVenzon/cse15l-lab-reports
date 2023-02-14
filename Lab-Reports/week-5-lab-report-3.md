# CSE 15L Week 5 Lab Report: Researching Commands (grep)

*Ian Venzon - Thursday 12:00 PM - B270*

## The grep command:

In this lab report, the command we will be taking a look at is `grep`. The `grep` command takes in a patten, then searches a file for the given pattern. It will then display all of the lines that contain said pattern. The syntax for `grep` is given by the following:

```
grep [options] pattern [files]
```

Source: [GeeksForGeeks: grep command in Unix/Linux](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)

There are a lot of different command line options for `grep` that can give us specific results. This is what we will be exploring in this lab report.

## Command line option #1: `-l`

If all we are interested in our search is the exact number of files that contain our desired pattern, then the `-l` command line option is very useful. The `-l` command makes it so `grep` only return the names of the files that match our search. For example, if I wanted to find how many files within the `./written_2/travel_guides/berlitz1/` directory contained the word "vista", I could use `-l` as such:

```
grep -l "vista" written_2/travel_guides/berlitz1/*.txt
```

![Image](https://i.imgur.com/3vqe1eN.png)

However, the `-l` option has its limits. If we only want to search through one file, it can't really tell us much. In this example, `find-results.txt` contains the results of running `$ find written_2` in the terminal. If we wanted to, we could use `-l` in the following way to check to see if `find-results.txt` has certain words or phrases within it.

![Image](https://i.imgur.com/N5pPEp8.png)

As you can see though, the viability of this is limited, as `-l` will simply return the file name which we are searching through if a match has been found, or nothing if a match was not found.

## Command line option #2: `-c`

Another useful command line option for `grep` is `-c`, which counts the number of search matches within a specified file. Using the same `find-results.txt` file from before, we can use `-c` to count the number of .txt files within `./written_2`. This is useful, because the `find` command will also return directories, which aren't what we are looking for in this case.

```
grep -c ".txt" find-results.txt
```
![Image](https://i.imgur.com/N5pPEp8.png)
