# Regular Expressions

### Simple Regular Expression example

The simplest building block of any regular expression is a character. We can use grep to search for any particular character from within a text of any given non-binary file. For example, here is a content of our regex.txt sample file:

```
$ cat regex.txt 
grep stands for:  
global           
regular          
expression       
print
```

Now we can use grep to search for any character by providing it with a regular expression. Let's use grep to search for a character "e":
```
$ grep e regex.txt                                          
grep stands for:
regular
expression
```
As you can see from the example above, grep printed all lines comprising of at least one "e" character. We can now combine multiple characters to form a string "regu" and use grep to search for a string in the text:
```
$ grep regu regex.txt 
regular
```
To unleash the real power of regular expressions though, we need to form a regular expression from non-alphabetic ( meta-characters ) characters or from the combination of alphabetic and non-alphabetic characters. For example, what if you want to search all lines which begin with character "g"? For this we can use a caret symbol "^":
```
$ grep ^g regex.txt 
grep stands for:
global
```
This was just a fundamental example of more sophisticated regular expression. In this article, we will explain more regular expression's techniques as the one above in the more detail.

Concatenation
As you can see on our preceding example, the simplest regular expression can consist of an individual character. Hence a regular expression consisting of a single non-special character will match any given string containing that character. The nature of Regular Expressions permits for concatenation of multiple other Regular Expressions. Which means that a set of characters such as "press" will match any string that contains a substring formed by concatenation of several regular expressions "p","r","e","s" and "s".
```
$ cat regex.txt 
grep stands for:                                                                   
global                                                                             
regular                                                                            
expression                                                                         
print
```
```
$ grep press regex.txt 
expression
```

### Basic vs Extended Regular Expressions
GNU grep understands both, basic and extended regular expressions. The prime difference is that in basic regular expressions, the meta-characters: ?, +, {, |, (, and ) lose their special meaning. To give meta-characters its special meaning they need to be escaped with backslash character. Think over a following example:

Our regex.txt file now contains the following:
```
$ cat regex.txt 
global|regular|expression|print
Global Regular Expression Print
```
grep command assumes basic regular expression as a default. Therefore, the following linux command will print exclusively first line only considering that it contains substring "n|p":
```
$ grep "n|p" regex.txt 
global|regular|expression|print
```
The "|" alteration operator has its own special meaning, and that is logical OR. However, this special meaning was suppressed in the previous example since grep by default threats any regular expression as a basic regular expression. To make grep read extended regular expressions, we need to use option -E or simply use egrep instead of grep.
```
$ grep -E "n|p" regex.txt 
global|regular|expression|print
Global Regular Expression Print
OR
$ egrep "n|p" regex.txt 
global|regular|expression|print
Global Regular Expression Print
```
In the preceding example, we used grep with extended regular expression, and thus it displays both lines, which contain n OR p character. As said previously the meta-characters lost their special meaning when expressed as basic regular expressions, unless they are escaped with "\" character. Let's re-use our first example but this time, we escape the "|" character:
```
$ grep "n\|p" regex.txt 
global|regular|expression|print
Global Regular Expression Print
```
In this case alteration operator "|" retains its special meaning and acts as logical OR even though we did not use -E option or egrep.

We also said that when using egrep or -E option, grep presumes to be fed with Extended Regular Expressions. Because of that, if you escape a meta character in extended regular expression context it will lose its special meaning and behave as a literal character "|". If you followed up to here you will notice that this is again exact opposite of basic regular expressions.

Example:
```
$ egrep "n\|p" regex.txt 
global|regular|expression|print
```

### Bracket Expressions

Now, that we are acquainted with basics of regular expressions, we can engage our exploration into a more powerful and yet more complex nature of regular expressions. The first stop will be the use of "[" and "]" known as "Bracket Expressions". The story behind the "Bracket Expressions" is that any characters enclosed by "[" and "]" will match any single character in that list. Let's wrap a letter "e" with "[]" and see what happens:
```
$ cat regex.txt 
global|regular|expression|print
Global Regular Expression Print
$ grep [e]xpression regex.txt 
global|regular|expression|print
```
As you can see nothing unusual happened here. Our current regular expression merely matched keyword "expression" and grep therefore printed respective line. On that ground, the following regular expression will also do the same trick:
```
$ grep expression regex.txt 
global|regular|expression|print
```
The power of Bracket Expression comes when you want to match for example a single character in the "[]" list. This is demonstrated in the following example:
```
$ grep [eE]xpression regex.txt 
global|regular|expression|print
Global Regular Expression Print
```
Can you think of a way how to formulate a regular expression alternative to the above example without using "[ ] "? Such technique has been already shown earlier!

Using Bracket Expression it is also possible to express a logical NOT. For this we can use a caret symbol "^". In the following example, we use a regular expression to extract all lines holding any characters with the exclusion of characters "a" and "c".
```
$ cat regex.txt 
a
b
c
d
$ grep [^ac] regex.txt 
b
d
```

### Expression Range

Bracket expression also allows you to specify an expression range. Expression range comprises of minimum two characters separated by a hyphen. What it means, is that instead of [0123456789] we can simply use [0-9] or instead of [abc] we can use [a-c]. This is illustrated in the following regex example:
```
$ cat regex.txt 
a
b
c
d
$ grep [^a-c] regex.txt 
d
```
### Character Classes
What follows are pre-defined classes for you to use within bracket expressions.

[:alnum:] - Alphanumeric characters	[:alpha:] - Alphabetic characters
[:cntrl:] - Control characters.	[:digit:] - Digits: 0 1 2 3 4 5 6 7 8 9.
[:graph:] - Graphical characters	[:lower:] - Lower-case letters
[:print:] - Printable characters	[:punct:] - Punctuation characters
[:space:] - Space characters	[:upper:] - Upper-case letters
[:xdigit:] - Hexadecimal digits	
In the following regular expression example, we will use [:lower:] and [:space:] to print only lines, which contain lower-case letter(s) or space:
```
cat regex.txt 
1
2
3
A
b
c
,
  <-- space
$ grep [[:lower:][:space:]] regex.txt 
b
c
  <-- space
```
### Anchoring
Anchoring is a regular expression technique which engages caret ^ symbol and the dollar sign $ as meta-characters to match the empty string from the beginning and at the end of the line respectively.

Let's find all lines within /etc/services file, which start with string "ftp":
```
$ grep ^ftp /etc/services 
ftp-data        20/tcp
ftp             21/tcp
ftps-data       989/tcp                         # FTP over SSL (data)
ftps            990/tcp
```
As an opposite example we can use regex anchoring to find all lines ending with ftp:
```
$ grep ftp$ /etc/services 
zope-ftp        8021/tcp
```
NOTE:Do not mistake caret's ^ meaning with a caret symbol used within bracket expression as they have quite distinct significance in their respective context.

The Backslash Character and Special Expressions
There are numerous system tools, including grep, which support "Special Expressions" also known as word boundaries. Here are some Special Expression symbols supported by grep and many other system utilities:
```
\< - match empty string at the beginning of the word
\> - match empty string at the end of the word
\b - match empty string at the beginning and end of the word
\B - match except at the beginning or end of a word
```
Let's start with \< which will match empty string from the beginning of the word. Here is our tester file:
```
$ cat regex.txt 
RegularExpressions
Regular ExpressionsRegular Expressions
```
The following Regular Expression will match both lines because there is an empty string before word "Regular" on each line:
``
$ grep "\<Regular" regex.txt 
RegularExpressions
Regular ExpressionsRegular Expressions
```
The next example will only display second line considering that we use \> to match empty string also at the end of the word:
```
$ grep "\<Regular\>" regex.txt 
Regular ExpressionsRegular Expressions
```
The meaning of \b is similar, but it will match both, empty string from the beginning and end of the word:
```
$ grep "\bExpressions\b" regex.txt 
Regular ExpressionsRegular Expressions
```
Whereas \B will only match when not at the beginning or end of the word:
```
$ grep "\bExpressions\B" regex.txt 
Regular ExpressionsRegular Expressions
```
For completeness of this section here are some other special expressions available for grep. Please note that following symbols are simply an abbreviation of above-mentioned Character Classes:
```
\s - Match any whitespace characters (space, tab, etc.). alias [:space:]
\S - Match any character but whitespace (space, tab, etc.). alias [^[:space:]]
\w - Match any character in the range 0 - 9, A - Z and a - z alias [:alnum:]
\W - Match any character but the range 0 - 9, A - Z and a - z alias [^[:alnum:]]
```
Here are some examples of Character Classes abbreviations:
```
$ cat regex.txt 

abcd
1234
"
Match TAB:

$ grep "\s" regex.txt 
        
Match anything but white space:

$ grep "\S" regex.txt 
abcd
1234
"
Match all Alphanumeric characters:

$ grep "\w" regex.txt 
abcd
1234
Match all non-alphanumeric ( includes whitespace )characters:

$ grep "\W" regex.txt      
"
```

### Repetition
A regular expression may be followed by one or several repetition quantifiers. Before you continue with this section, please take a look at the table below:

? - The preceding item is optional and matched at most once
* - The preceding item will be matched zero or more times.
+ - The preceding item will be matched one or more times.
{n} - The preceding item is matched exactly n times.
{n,} - The preceding item is matched n or more times.
{n,m} - The preceding item is matched at least n times, but not more than m times.
Let's begin by creating our sample file regex.txt:

$ cat regex.txt 
Expressions
Expressssssions
Expresssions
Expresions
Expreions
First repetition example will use "?":

$ grep -E "Expres?ions" regex.txt 
Expresions
Expreions
As described in the table above, the usage of "?" quantifier is to match preceding item at most once or to make the previous item optional. The previous item in our case is a character "s". Therefore, grep matched only strings with none or single character "s" followed by string "ions". Next quantifier we are going to take a look at is "*" which by definition will match previous item zero or more times.

$ grep -E "Expres*ions" regex.txt 
Expressions
Expressssssions
Expresssions
Expresions
Expreions
As illustrated above the "*" quantifier will match all strings in our test file. If you wonder why it also matched "Expreions" keep in mind that the "*" quantifier makes the preceding item optional as opposed to "+" quantifier, which must match preceding item at least once or more times:

$ grep -E "Expres+ions" regex.txt 
Expressions
Expressssssions
Expresssions
Expresions
With the "{n}" quantifier you can specify precisely how many times the previous item will be matched. For example our:

$ grep -E "Expres{3}ions" regex.txt 
Expresssions
command will match string, which starts with "Expre" followed by 3 x "s" and followed by "ions". To stretch our previous regular expression "{n,}" futher, we can specify the minimum value of how many times the preceding item will be matched. As a result, "{3,}" repetition would match 3 or more times:

$ grep -E "Expres{3,}ions" regex.txt 
Expressssssions
Expresssions
To extend the above regular expression even further we can specify range. Therefore, we replace "{3,}" with "{1,3}" and the following regex would match:

$ grep -E "Expres{1,3}ions" regex.txt 
Expressions
Expresssions
Expresions
since the previous item "s" is matched at the minimum once but no more than three times.

Alternation
You can think of regex alternation as a logical OR operation where regular expressions can be joined together by one or more "|" alteration operators. As a result, this regular expression will match any string corresponding to either alternate regular expression.

$ cat regex.txt                                   
grep stands for:                                                                                  
global                                                                                            
regular                                                                                           
expression                                                                                        
print                                                                                             
$ grep -E "^r|^e" regex.txt                                                
regular                                                                            
expression
Precedence
When forming expressions, there is another property of Regular Exppresisons to consider and that is precedence. Similar as it is with arithmetic calculations, regular expressions follow predefined precedence. The highest precedence takes "Repetition" followed by "Concatenation" and the lowest precedence belongs to "Alternation". Consider a following example:

$ cat regex.txt 
regex
regexxx
$ grep -E "regex{3}" regex.txt 
regexxx
In the aforementioned regular expression, we can see both, Concatenation "regex" and Repetition "x{3}". Since the repetition has higher precedence the above regular expression will match "regexxx" but not "regex".
Another example where precedence needs to be taken into account is when using Alteration operator "|" which has the lowest precedence from all regular expressions. Consider a following example:

$ cat regex.txt 
regular expressions
regular
expressions
$ grep -E "^regular|expressions$" regex.txt 
regular expressions
regular
expressions
Since the alteration operator "|" has lowest precedence the above regular expression will match any concatenated expression. In our case, it will be "regular" with anchor "^" and "expressions" with an end of the line anchor "$". In order to give any regex operator higher precedence we need to use "()". In the following example, we will use "()" to override Alteration operator precedence to a higher priority, which makes noticeable difference:

$ grep -E "^(regular|expressions)$" regex.txt 
regular
expressions
In this example, the alteration operator is evaluated first as it creates a simple subexpression using "()". Therefore, as a result the above regular expression will only match lines, which contain "^regular$" OR "^expressions$".

Back References and Subexpressions
Any substring folded by "()" will create a subexpression which can be used as a back reference in succeeding regular expression. This is illustrated by the following example:

$ cat regex.txt 
regular expressions
$ grep -E "(re)gular expssions" regex.txt
regular expressions
Subexpression of concatenated regular expression "re" is used as a back reference later when forming regular expression by use of \1 digit. The order used to form subexpressions "n" needs to be consistent with back reference "\n":

$ grep -E "(r)(e)gular xpssions" regex.txt
regular expressions
Conclusion
Regular expressions are very powerful tool in hands of any system admin, programmer ( BASH, PHP, C#, Java and many more.. ) or casual Linux/Unix command line user. This article attempted to describe in some simple, consistent and plain English manner the basics of Regular Expressions upon which you can further develop your Regular Expressionsskills and thus save yourself from tedious work which text processing can sometimes offer.
