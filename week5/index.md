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

For example, if I wanted to find all files with paths containing an "O", I could do 
```
$ find written_2/ -name "*O*"
written_2/travel_guides/berlitz2/NewOrleans-History.txt
written_2/NewOrleans-History.txt
written_2/chO.txt
written_2/non-fiction/OUP
written_2/non-fiction/OUP/Castro/chO.txt
```

But this returns directories as well. Using `-type f`, we only find the files with paths containing an "O"
```
$ find written_2/ -name "*O*" -type f
written_2/travel_guides/berlitz2/NewOrleans-History.txt
written_2/NewOrleans-History.txt
written_2/chO.txt
written_2/non-fiction/OUP/Castro/chO.txt
```








