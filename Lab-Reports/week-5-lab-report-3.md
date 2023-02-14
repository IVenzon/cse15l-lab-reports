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
![Image](https://i.imgur.com/B2XIrtW.png)

From our search, we can see that there are 179 .txt files within `./written_2`.

## Command line option #3: `-i`

One limitation of the `grep` command is that it only searches for and returns exact matches. Consider the following situation: Say I wanted to count the number of times the word "physics" appears in **ANY form** within `./written_2/non-fiction/OUP/Kauffman`? I could use the following command to try and find out:

![Image](https://i.imgur.com/FJIUdoL.png)

However, this doesn't account for any occurences of "physics" with a capital P ("Physics"). I could find all instances of "Physics" with the following:

![Image](https://i.imgur.com/zDbTdAg.png)

As we can see, our first search missed one instance within `ch5.txt`! We could add up the values from each search, but this doesn't seem very efficient. A more elegant solution is the `-i` command line option. `-i` will make our search *case insensitive*, which allows us to do our original search in a single line.

```
grep -c -i "PHYSICS" written_2/non-fiction/OUP/Kauffman/*.txt
```
![Image](https://i.imgur.com/cfTHYjP.png)

Now both the "physics" and "Physics" within `ch5.txt` are counted in our search.

## Command line option #4: `-r`

Another big limitation of `grep` is that we can only use it on files. Attempting to use `grep` on a directory simply results in an error.

![Image](https://i.imgur.com/ytF9rAb.png)

This is not a big deal if we only need to look through a single directory, but what if we wanted to search through multiple? This is where the `-r` command line option comes in. The `-r` command line option turns our search into a *recursive search*. This means that our search will look through the given directory and all of its subdirectories too.

Let's look back to one of the earlier examples where we searched for all files which contained "vista" within `./written_2/travel_guides/berlitz1/`. What if we wanted to find all occurences of "vista" within the `/travel_guides` directory as a whole? To do so, we could use `-r` like so:

```
grep -l -r "vista" written_2/travel_guides/
```
![Image](https://i.imgur.com/dvwU2FC.png)

Here we see that there are 20 files in total that contain the word "vista", 10 being the ones we found within `/berlitz1` from our original search, and an additional 10 files which were within `/berlitz2`.

The `-r` command is also very useful in combination with other commands. Here, the `-i` and `-l` commands are used in conjunction with `r` to find all of the files which contain some variation of the word "simply" within `./written_2/non-fiction`.

```
grep -r -i -l "SIMPLY" written_2/non-fiction/
```

![Image](https://i.imgur.com/zlNUOAY.png)
