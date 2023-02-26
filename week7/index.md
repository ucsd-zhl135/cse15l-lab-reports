## Lab Report 4

For the competition, I used the strategy of combining all the steps 5-9 into one command with semicolons, which I stored in the bash history on `ieng6`, and could access quickly.

The commands needed were
```
git clone git@github.com:ucsd-zhl135/lab7.git
cd lab7
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples
sed -i "43s/index1/index2/g" ListExamples.java
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples
git add -A && git commit -m "a" && git push
```

So I combined them into the following:
```
git clone git@github.com:ucsd-zhl135/lab7.git ; cd lab7 ; javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java ; java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples ; sed -i "43s/index1/index2/g" ListExamples.java ; javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java ; java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples ; git add -A ; git commit -m "a" ; git push
```

And I also stored the ssh command for step 4 in the bash history of my local machine. 

So for step 4:
`
Keys pressed: <up><enter>

This ran the command `ssh cs15lwi23adl@ieng6.ucsd.edu`, which automatically logged me into my ieng6 account as I had ssh keys set up.
`

And for step 5-9:
```
Keys pressed: <up><up><enter>

This ran the command `git clone git@github.com:ucsd-zhl135/lab7.git ; cd lab7 ; javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java ; java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples ; sed -i "43s/index1/index2/g" ListExamples.java ; javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java ; java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples ; git add -A ; git commit -m "a" ; git push`, which completed all the steps in sequence.
```

