# *Find* command

## *-name* option

```
[cs15lwi23akn@ieng6-201]:skill-demo1-data:203$ find written_2 -name "WhereToE*.txt"
written_2/travel_guides/berlitz1/WhereToEdinburgh.txt
written_2/travel_guides/berlitz1/WhereToEgypt.txt
```
- In the above snippet we use *find's -name* option and pass in the argument "WhereToE*.txt"
- This command finds and returns the names of all txt files with the name pattern "WhereToE" in the *written_2* directory
- As we can see from above, it returned two txt files. One named "WhereToEdinburgh" and "WhereToEgypt"
- This allows us to find a list of files in a directory that have a certain name pattern quickly

```
[cs15lwi23akn@ieng6-201]:skill-demo1-data:207$ find written_2 -name "berlitz*"
written_2/travel_guides/berlitz1
written_2/travel_guides/berlitz2
```
- In the above snippet, we pass the argument *berlitz** instead of "WhereToE*.txt"
- This means that we want to find all files AND directories that contain/start with berlitz except this time the files don't have to be .txt files
- The command ended up returning the directories berlitz1 and berlitz2
- This means that we can use the *find* command to find both files of all sorts of types and directories that have a certain name pattern

Source: ChatGPT (https://chat.openai.com/chat/) using the prompt : "give me options for the bash command find that i can use on files and directories"

## *-type*

```
[cs15lwi23akn@ieng6-201]:skill-demo1-data:218$ cd written_2/non-fiction/OUP/Kauffman 
[cs15lwi23akn@ieng6-201]:Kauffman:219$ echo "" >> test.java
[cs15lwi23akn@ieng6-201]:Kauffman:225$ mkdir java
[cs15lwi23akn@ieng6-201]:Kauffman:221$ cd ../../../..
[cs15lwi23akn@ieng6-201]:skill-demo1-data:229$ find written_2/ -type f -name "*java"
written_2/non-fiction/OUP/Kauffman/test.java
```
- For the sake of this example, I changed the current directory to "Kauffman" and created both a java file named "test.java" as well as a subdirectory called "java"
- I passed the arguments *f* to *-type* and **java* to *-name*
- This means that *find* should return files (and not directories) with names that contain "java"
- The command ended up only returning "test.java" and not java the directory
- This option can help prevent any naming conflict between files and directories

```
[cs15lwi23akn@ieng6-201]:skill-demo1-data:238$ find written_2/ -name "*java"
written_2/non-fiction/OUP/Kauffman/test.java
written_2/non-fiction/OUP/Kauffman/java
[cs15lwi23akn@ieng6-201]:skill-demo1-data:238$ find written_2/ -type d -name "*java"
written_2/non-fiction/OUP/Kauffman/java
```
- Without the option *-type d* we can see that *find* outputs both the .java file and the java directory
- With *-type d*, with *d* meaning directories, only the java directory is returned
- Files and directories that have similar or exactly the same names can be differientated from one another with *-type*
- If we don't use the *-name* option in conjunction, *-type* can be used to separate files in a directory from subdirectories

Source: ChatGPT (https://chat.openai.com/chat/) using the prompt : "give me options for the bash command find that i can use on files and directories"

## *-size*

```
[cs15lwi23akn@ieng6-201]:skill-demo1-data:239$ find written_2/ -size 5       
written_2/travel_guides/berlitz1/WhatToFrance.txt
written_2/travel_guides/berlitz1/WhatToHawaii.txt
written_2/travel_guides/berlitz1/WhereToHawaii.txt
[cs15lwi23akn@ieng6-201]:skill-demo1-data:254$ wc -c < written_2/travel_guides/berlitz1/WhatToFrance.txt
2324
```
- I pass the argument *5* to *-size* which means *find* will return the names of all files that have around 4 to 5 blocks of 512 byte blocks
- Three files were returned and I verified the size of one of the files using *wc -c* (*-c* returns byte count) which returned 2324 bytes
- 2324 divided by 512 is a little bit more than 4.5 which matches closely to our argument of 5
- *-size* can help us find very large files that perhaps take up too much space on our storage/drives

```
[cs15lwi23akn@ieng6-201]:skill-demo1-data:279$ find written_2/ -size +400
written_2/travel_guides/berlitz1/WhereToFrance.txt
written_2/travel_guides/berlitz1/WhereToItaly.txt
written_2/travel_guides/berlitz2/Canada-WhereToGo.txt
```
- I passed the argument *+400* to *-size* which means find should only return files in "written_2" that are GREATER than 400 blocks of 512 byte blocks
- It returned only three .txt files which means these files are the largest files in the directory
- As stated above *-size* can help us filter out files that are very large for purposes like deletion, modification, or transfer elsewhere

Sources: 
- ChatGPT (https://chat.openai.com/chat/) using the prompt "give me options for the bash command find that i can use on files and directories"
- Used to determine valid arguments: https://linuxconfig.org/how-to-use-find-command-to-search-for-files-based-on-file-size

## *-maxdepth*

```
[cs15lwi23akn@ieng6-201]:skill-demo1-data:295$ find written_2/ -maxdepth 1 
written_2/
written_2/non-fiction
written_2/travel_guides
```
- I passed the argument *1* to *-maxdepth* which means *find* should only return the files in only 1 level deep into the "written_2" directory
- As expected it returned both the "non-fiction" and "travel_guides" directories in "written_2"
- This allows us to pipe all the files of a certain level in the directory hierachy without having to change the current working directory or pasting tons of file paths

```
[cs15lwi23akn@ieng6-201]:skill-demo1-data:296$ find written_2/ -maxdepth 2
written_2/
written_2/non-fiction
written_2/non-fiction/OUP
written_2/travel_guides
written_2/travel_guides/berlitz1
written_2/travel_guides/berlitz2
```
- Passing the argument *2* to *-maxdepth* means it should return all files in the 2nd level fo the directory hierarchy
- The 2nd level should be all of the files in "non-fiction" and "travel_guides" which is exactly what *find* with *-maxdepth* returned
- Additionally to being easier to pipe files as arguments, *-maxdepth* can also give us multiple paths and file names without having to change multiple directories

Source: ChatGPT (https://chat.openai.com/chat/) using the prompt "give me options for the bash command find that i can use on files and directories"
