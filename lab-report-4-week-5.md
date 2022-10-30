__Week 5 Lab Report Blog - File Manipulation__

We are going to examine the command "grep"

__grep -o__
One alternate version of grep that we can use is grep -o, which will only display the matched parts of a matching line.

__Example 1:__
__The file grep-o.sh:__
```
set -e

grep -o "base pair" technical/$1/* > onlyWords.txt

wc onlyWords.txt
```

__Command line input and output:__
```
ericnguyen@Erics-MacBook-Pro-3 docsearch-fork % bash grep-o.sh plos
       3       6     150 onlyWords.txt
```
This command is counting how many times the words "base pair" appear within all the files in the plos directory. From the command line, it appears that the words appear 6/2 = 3 times.

__Example 2:__
__Updated file grep-o.sh__
```
set -e

grep -o "biology is" technical/$1/* > onlyWords.txt

wc onlyWords.txt
```

__Command line input and output:__
```
ericnguyen@Erics-MacBook-Pro-3 docsearch-fork % bash grep-o.sh biomed
       6      12     302 onlyWords.txt
```
This command counts how many times the words "biology is" appears within the files in the directory biomed. It seems to have appeared 12/2 = 6 times.

__Example 3__
__Updated file grep-o.sh__
```
set -e

grep -o "this is a" technical/$1/* > onlyWords.txt

wc onlyWords.txt
```

__Command line input and output__
```
ericnguyen@Erics-MacBook-Pro-3 docsearch-fork % bash grep-o.sh government/Alcohol_Problems
       1       3      65 onlyWords.txt
```
This command counts how many times the phrase "this is a" appears in the files within the subdirectory Alcohol_Problems. It seems to have appeared 3/3 = 1 time.



__grep -v__
grep -v will return the lines within a directory/file that do not contain the phrase given in the argument.

__Example 4:__
__Updated file grep-i.sh:__
```
set -e

grep -v "bio" technical/$1/* > notThese.txt

wc notThese.txt
```

__Command line input and output:__
```
ericnguyen@Erics-MacBook-Pro-3 docsearch-fork % bash grep-v.sh biomed
  487426 3899983 43764112 notThese.txt
```
This command shows that 487426 lines in all of the files in the biomed directory do not contain the word/subphrase "bio".

__Example 5:__
__Updated file grep-i.sh:__
```
set -e

grep -i "biology is" technical/$1/* > notThese.txt

wc notThese.txt
```

__Command line input and output:__
```
ericnguyen@Erics-MacBook-Pro-3 docsearch-fork % bash grep-i.sh plos
      10     141    1320 notThese.txt
```
This command shows that 10 lines in all of the files in the plos directory do not contain the phrase "biology is."

__Example 6:__
__The file grep-i.sh:__
```
set -e

grep -v "problem" technical/$1/* > notThese.txt

wc notThese.txt
```

__Command line input and output:__
```
ericnguyen@Erics-MacBook-Pro-3 docsearch-fork % bash grep-v.sh government/Alcohol_Problems
    3955   33439  441909 notThese.txt
```
This command shows how many lines in the files in the Alcohol_Problems subdirectory don't contain the word "problem": 3955.



__grep a__