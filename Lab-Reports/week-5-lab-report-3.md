# CSE 15L Week 5 Lab Report: Researching Commands (grep)

*Ian Venzon - Thursday 12:00 PM - B270*

## The `grep` command:

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

Using `grep` and `-l` like could be useful if you had all of your notes in a single directory and wanted to search for specific key phrases/concepts, as it would give you a specific list of which files have the content you want to study.

Source: [15 Practical Grep Command Examples In Linux / UNIX](https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)

However, the `-l` option has its limits. If we only want to search through one file, it can't really tell us much. In this example, `find-results.txt` contains the results of running `$ find written_2` in the terminal. If we wanted to, we could use `-l` in the following way to check to see if `find-results.txt` has certain words or phrases within it.

```
grep -l "travel" find-results.txt             //should return something!

grep -l "nothing!" find-results.txt           //should return nothing!
```

![Image](https://i.imgur.com/N5pPEp8.png)

As you can see though, the viability of this is limited, as `-l` will simply return the file name which we are searching through if a match has been found, or nothing if a match was not found.

Source: [15 Practical Grep Command Examples In Linux / UNIX](https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)

## Command line option #2: `-c`

Another useful command line option for `grep` is `-c`, which counts the number of search matches within a specified file. Using the same `find-results.txt` file from before, we can use `-c` to count the number of .txt files within `./written_2`. This is useful, because the `find` command will also return directories, which aren't what we are looking for in this case.

```
grep -c ".txt" find-results.txt
```
![Image](https://i.imgur.com/B2XIrtW.png)

From our search, we can see that there are 179 .txt files within `./written_2`.

`-c` is useful in situations where we are parsing through a large amount of data and all we care about is the frequency of a certain result. Imagine trying to count 179 .txt files by hand!

Source: [15 Practical Grep Command Examples In Linux / UNIX](https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)

The `-c` command can also apply to multiple files in a single search. If multiple files are searched, `grep` will first list out the name of the file and then list the number of search matches within said file. This can be seen below, where `-c` was used to find the number of times "architect" appears within `./written_2/non-fiction/OUP/Rybczynski`.

```
grep -c "architect" written_2/non-fiction/OUP/Rybcynzski/*.txt
```
![Image](https://i.imgur.com/pw0NxMP.png)

Using `-c` in this way could be useful in trying to analyze certain speech/writing habits within a text. For example, if you had the transcribed speeches of 30 different people, you could use `-c` to find out how many times they use filler words such as "um".

Source: [15 Practical Grep Command Examples In Linux / UNIX](https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)

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

Now both the "physics" and "Physics" within `ch5.txt` are counted in our search. Make sure to use `-i` if you want to catch **EVERY** instance of your search phrase, as just regular `grep` might not catch everything.

Source: [15 Practical Grep Command Examples In Linux / UNIX](https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)

However, whenever we use `-i`, we need to be careful. By default, `grep` will also return a match if the search pattern is a *substring* within a word. If I used `grep -i "rot"` to try and find all instances of the word "rot", I would get a false positive if the file contained the word "carrot", as "rot" is a substring within "carrot". We can fix this by simply changing `-i` to `-iw`, which makes it so our search will only return matches for the specified word.

Here, I am using just `-i` to search `./written_2/non-fiction/OUP/Fletcher/ch2.txt` for the word "is". 

![Image](https://i.imgur.com/QPBXFmw.png)

Now, I am doing the exact same search, but using `-iw` to make sure we only catch instances of "is" and no words where "is" is a substring.

```
grep -iw -c "is" written_2/non-fiction/OUP/Fletcher/ch2.txt
```
![Image](https://i.imgur.com/RpwQIFf.png)

In total, using just `-i` gave us 35 false positives! This is why it is important to keep in mind what exactly you are searching. If you are searching for something very specific or long, then `-i` should be just fine. If you are searching for something very small or you know it is a common prefix/suffix/substring for other words, consider using `-iw` to get a more accurate result.

Source: [15 Practical Grep Command Examples In Linux / UNIX](https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)

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

Source: [15 Practical Grep Command Examples In Linux / UNIX](https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)

The `-r` command is also very useful in combination with other commands. Here, the `-i` and `-l` commands are used in conjunction with `r` to find all of the files which contain some variation of the word "simply" within `./written_2/non-fiction`.

```
grep -r -i -l "SIMPLY" written_2/non-fiction/
```

![Image](https://i.imgur.com/zlNUOAY.png)

All in all, the `-r` command makes using `grep` a lot easier on us. Instead of having to use `grep` multiple times for each directory, we can simply use `-r` and let recursive `grep` do all the work for us.

Source: [15 Practical Grep Command Examples In Linux / UNIX](https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)
