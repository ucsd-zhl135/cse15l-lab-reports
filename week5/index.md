## Lab Report 3

We will be looking at the `find` command. 

First, we can consider the `-exec` argument. This argument executes a command for every file that is found by `find`. For example, to search every text file in `written_2` for the string "among us", we can do the following:
```
[thomas@linux-desktop skill-demo1-data]$ find written_2/ -name "*.txt" -exec grep -l "among us" {} \;
written_2/non-fiction/OUP/Kauffman/ch9.txt
written_2/non-fiction/OUP/Kauffman/ch7.txt
written_2/non-fiction/OUP/Berk/CH4.txt
```
Of course, we could achieve the same thing with the `-r` argument of `grep`, but this is an alternative way. 



