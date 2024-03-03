# Combining outputs from du and ls

We use `du` command to show the size of the directories, but it cannot show the owner of the directories as `ls`.

```
$ du -h --summarize --human-readable --total * | sort -hr
8.2T    total
866G    Project_A
773G    Project_D
734G    Project_B
372G    Project_C
233G    Project_E
...
```

```
$ ls -ahl
drwxrwxr-x 2 user1  lab 4.0K Jan  9 14:18 Project_A
drwxrwxr-x 2 user2  lab 4.0K Jan  9 14:17 Project_C
drwxrwxr-x 5 user1  lab 4.0K May 18  2022 Project_B
drwxrwxr-x 2 user2  lab 4.0K Dec  1 10:11 Project_D
drwxrwxr-x 4 user2  lab 4.0K Mar  8 11:20 Project_E
...
```

How can I combine these two outputs together so that I can see the size and the owner of the directories at the same time?

Here is the trick:

```
join -1 2 -2 9  <(du -h --summarize --human-readable --total *) <(ls -ahl)
```

* [`join`](https://www.geeksforgeeks.org/join-command-linux/) is used to combine the lines of two files on a common field.
* We join them by field 2 in file 1 (output from `du` command) and field 9 in file 2 (output from `ls`).

And we can make it nicer by:

```
join -1 2 -2 9  <(du -h --summarize --human-readable --total *) <(ls -ahl) | column -t | cut -f 1,2,3,5,8,9,10 | sort -k 2,2 -hr
```

* `column` replaces the space with a tab for a nicer appearance.
* `cut` selects the columns I need.
* `sort` ranks the lines by their size.

### Reference

* [combine output from 2 linux commands into one output](https://stackoverflow.com/questions/34658993/combine-output-from-2-linux-commands-into-one-output)
