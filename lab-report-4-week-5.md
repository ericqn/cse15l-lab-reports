__Week 5 Lab Report Blog - File Manipulation__

We are going to examine the command "grep"

---

__grep -o__
One alternate version of grep that we can use is grep -o, which will only display the matched parts of a matching line. This version of grep could potentially be helpful in finding how many words match the inputted word argument without having to print the entire line.

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

---

__grep -v__
grep -v will return the lines within a directory/file that do not contain the phrase given in the argument. Grep -v can be used as the opposite of the regular grep statement. IF we want to exclude any phrases or words in a specific document, we can use grep -v.

__Example 4:__
__Updated file grep-v.sh:__
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
__The file grep-v.sh:__
```
set -e

grep -v "biology is" technical/$1/* > notThese.txt

wc notThese.txt
```

__Command line input and output:__
```
ericnguyen@Erics-MacBook-Pro-3 docsearch-fork % bash grep-v.sh plos
      10     141    1320 notThese.txt
```
This command shows that 10 lines in all of the files in the plos directory do not contain the phrase "biology is."

__Example 6:__
__Updated file grep-i.sh:__
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

---

__grep -i__
This command line version of grep ignores whether or not the argument or line searched for is lowercase or uppercase. This allows a higher degree of search. Sometimes, we want case-specific words, and other times, we just want to find a general word or locate the word if we forgot which cases are upper and lower in the word. Grep -i can be used for this.

__Example 7:__
__The file grep-i.sh:__
```
set -e

grep -i "YOI" technical/$1/* > upperlower.txt

wc upperlower.txt
```

__Command line input and output:__
```
ericnguyen@Erics-MacBook-Pro-3 docsearch-fork % bash grep-i.sh biomed
      15     126    1542 upperlower.txt
```
We look through the directory biomed for the subphrase "yoi", where the case of the character does not matter. This returns 15 lines throughout all of the files in the biomed directory.

__Example 8:__
__Updated file grep-i.sh:__
```
set -e

grep -i "fOUr" technical/$1/* > upperlower.txt

wc upperlower.txt
```

__Command line input and output:__
```
ericnguyen@Erics-MacBook-Pro-3 docsearch-fork % bash grep-i.sh plos
      52     742    6454 upperlower.txt
```
We look through the directory plos for the word "fOUr", where the case of the character does not matter. Doing this without the case-insensitive command would most likely return zero files.

__Example 9:__
__Updated file grep-i.sh:__
```
set -e

grep -i "ripper" technical/$1/* > upperlower.txt

wc upperlower.txt
```

__Command line input and output:__
```
ericnguyen@Erics-MacBook-Pro-3 docsearch-fork % bash grep-i.sh biomed
       2      21     204 upperlower.txt
```
We look through the directory biomed for the word "ripper", where the search is case-insensitive. Surprisingly, I find 2 lines with this word or string of characters.