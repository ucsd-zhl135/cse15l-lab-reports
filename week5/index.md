## Lab Report 3

We will be looking at the `find` command. 

First, we can consider the `-exec` argument. This argument executes a command for every file that is found by `find`. For example, to find every text file in `written_2` with the string "among us", we can do the following:
```
$ find written_2/ -name "*.txt" -exec grep -l "among us" {} \;
written_2/non-fiction/OUP/Kauffman/ch9.txt
written_2/non-fiction/OUP/Kauffman/ch7.txt
written_2/non-fiction/OUP/Berk/CH4.txt
```
Of course, we could achieve the same thing with the `-r` argument of `grep`, but this is an alternative way. Note that {} represents the current file name, while ; denotes the end of the command to be executed. It needs to be escaped with \ to be registered. 

We could also use this to copy all the files with a certain name to a directory, like the following, which copies all the text files to `written_2`: 
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






