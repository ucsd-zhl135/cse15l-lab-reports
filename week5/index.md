## Lab Report 3

We will be looking at the `find` command. 

First, we can consider the `-exec` argument. I learned about this from the site https://www.redhat.com/sysadmin/linux-find-command. This argument executes a command for every file that is found by `find`. For example, to find every text file in `written_2` with the string "among us", we can do the following:
```
$ find written_2/ -name "*.txt" -exec grep -l "among us" {} \;
written_2/non-fiction/OUP/Kauffman/ch9.txt
written_2/non-fiction/OUP/Kauffman/ch7.txt
written_2/non-fiction/OUP/Berk/CH4.txt
```
Of course, we could achieve the same thing with the `-r` argument of `grep`, but this is an alternative way. Note that {} represents the current file name, while ; denotes the end of the command to be executed. It needs to be escaped with \ to be registered. 

We could also use this to copy all the files with a certain name to a directory, like the following, which copies all the text files in the subdirectories to `written_2`: 
```
$ find written_2/ -name "*.txt" -exec cp {} written_2/ \;
$ ls written_2/
Algarve-History.txt      California-History.txt       chQ.txt                   HistoryFrance.txt        IntroLasVegas.txt         WhatToIndia.txt
Algarve-Intro.txt        California-WhatToDo.txt      chR.txt                   HistoryFWI.txt           IntroLosAngeles.txt       WhatToIsrael.txt
Algarve-WhatToDo.txt     California-WhereToGo.txt     chV.txt                   HistoryGreek.txt         IntroMadeira.txt          WhatToIstanbul.txt
Algarve-WhereToGo.txt    Canada-History.txt           chW.txt                   HistoryHawaii.txt        IntroMadrid.txt           WhatToItaly.txt
Amsterdam-History.txt    Canada-WhereToGo.txt         chY.txt                   HistoryHongKong.txt      IntroMalaysia.txt         WhatToJamaica.txt
...
```
These commands could be used manage files efficiently, such as separating user files from auto-generated files. 

Next, we can consider the `-type` argument. I found this from the site https://linuxhandbook.com/find-command-examples/. We can use this to only return files, or only return directories. For example, 
```
$ find written_2/ -type d
written_2/
written_2/travel_guides
written_2/travel_guides/berlitz1
written_2/travel_guides/berlitz2
written_2/non-fiction
written_2/non-fiction/OUP
written_2/non-fiction/OUP/Fletcher
written_2/non-fiction/OUP/Castro
written_2/non-fiction/OUP/Rybczynski
written_2/non-fiction/OUP/Kauffman
written_2/non-fiction/OUP/Berk
written_2/non-fiction/OUP/Abernathy
```
This command returned all the directories in `written_2/`. This could be used to avoid errors when using the output of `find` in other commands such as grep, as you could only find files and avoid directories.

For example, if I wanted to find all files with names containing an "O", I could do 
```
$ find written_2/ -name "*O*"
written_2/travel_guides/berlitz2/NewOrleans-History.txt
written_2/NewOrleans-History.txt
written_2/chO.txt
written_2/non-fiction/OUP
written_2/non-fiction/OUP/Castro/chO.txt
```

But this returns directories as well. Using `-type f`, we only find the files with names containing an "O"
```
$ find written_2/ -name "*O*" -type f
written_2/travel_guides/berlitz2/NewOrleans-History.txt
written_2/NewOrleans-History.txt
written_2/chO.txt
written_2/non-fiction/OUP/Castro/chO.txt
```

We can also search for files of a given size with the `-size` argument. I also learned this from https://linuxhandbook.com/find-command-examples/. For example, to find all the files that greater than 200 KB in size,
```
$ find written_2/ -size +200k
written_2/Canada-WhereToGo.txt
written_2/travel_guides/berlitz1/WhereToFrance.txt
written_2/travel_guides/berlitz1/WhereToItaly.txt
written_2/travel_guides/berlitz2/Canada-WhereToGo.txt
written_2/WhereToFrance.txt
written_2/WhereToItaly.txt
```
The + specifices that we want greater than 200 KB. To find files less than a given size, we use -:
```
$ find written_2/ -size -2k
written_2/travel_guides/berlitz1/HandRIstanbul.txt
written_2/travel_guides/berlitz1/HandRIbiza.txt
written_2/HandRIstanbul.txt
written_2/HandRIbiza.txt
```

This finds the files that are smaller than 2 KB. If we don't use + or -, we want files that are exactly a given size.

Lastly, we can search for files with multiple conditions with the `-o` argument. I also learned this from https://linuxhandbook.com/find-command-examples/. For example, to find files with names containing "Cal" or "Can",
```
$ find written_2/ -name "*Cal*" -o -name "*Can*"
written_2/travel_guides/berlitz2/CanaryIslands-History.txt
written_2/travel_guides/berlitz2/CanaryIslands-WhereToGo.txt
written_2/travel_guides/berlitz2/Canada-WhereToGo.txt
written_2/travel_guides/berlitz2/Cancun-WhereToGo.txt
written_2/travel_guides/berlitz2/Canada-History.txt
written_2/travel_guides/berlitz2/Cancun-WhatToDo.txt
written_2/travel_guides/berlitz2/California-History.txt
written_2/travel_guides/berlitz2/California-WhereToGo.txt
written_2/travel_guides/berlitz2/CanaryIslands-WhatToDo.txt
written_2/travel_guides/berlitz2/California-WhatToDo.txt
written_2/travel_guides/berlitz2/Cancun-History.txt
```
We can also combine other arguments such as `-type` to search for files with names containing "Cal" or directories.
```
$ find written_2/ -name "*Cal*" -o -type d
written_2/
written_2/travel_guides
written_2/travel_guides/berlitz1
written_2/travel_guides/berlitz2
written_2/travel_guides/berlitz2/California-History.txt
written_2/travel_guides/berlitz2/California-WhereToGo.txt
written_2/travel_guides/berlitz2/California-WhatToDo.txt
written_2/California-History.txt
written_2/California-WhereToGo.txt
written_2/California-WhatToDo.txt
written_2/non-fiction
written_2/non-fiction/OUP
written_2/non-fiction/OUP/Fletcher
written_2/non-fiction/OUP/Castro
written_2/non-fiction/OUP/Rybczynski
written_2/non-fiction/OUP/Kauffman
written_2/non-fiction/OUP/Berk
written_2/non-fiction/OUP/Abernathy
```

This argument is useful to search for things more generally, like if I wanted to list all the files in a directory that are source code, I could combine extensions with `-o`. 




