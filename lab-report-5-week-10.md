# **Lab Report 5 - MarkdownParse Tests and Results**

## **First Test/Issue**
---

The first test was technically a complete fail by my code. Every test failed
against my code, and returned an IndexOutOfBoundsError.

[Here](https://github.com/heter13/markdown-parse/commit/5675aab158f4259f75460be93c18b667507836af)
is the original state of my code.

While the bug was unfortunate, it was fortunately very easy to discern the
difference between the results for both implementations of MarkDownParse.

Since my code resulted in an error thrown, that means that there was no output 
for any of the test files. Since that is the case, that means that all 652 
test files had to have different outputs.

The issue with my code (which we tested and fixed in lab) was the way I ignore 
out of bounds indexes. The code originally just had a line to ensure that the
current index was not 0 (so as to avoid links at the beginning of the file 
causing issues). Instead, we changed that to an if statement to ensure that
none of the variables were equal to -1 at any point during the iteration.

[Here](https://github.com/heter13/markdown-parse/blob/main/MarkdownParse.java)
is the updated code.

## **Tests**
---

Now that the code has been updated, we can see how the implementation really 
stacks up against the main MarkdownParse implementation.

For this section I am going to be looking at test files 567 and 520.

567:
```
[foo](not a link)

[foo]: /url1
```
520:
```
*[foo*](/uri)
```

Outputs:

My implementation:
```
[not a link]
[/uri]
```

Main implementation:
```
[]
[/uri]
```

For these two files, the proper output for both would be `[]`, since there is 
no real link in either file. That means that my implementation was wrong for
567, and both implementations were wrong for 520.

The issue with my code is that I left in the else statement, which means that 
even if the code doesn't meet the requirements in the else if statement, it 
will still be added to the list.

Delete:

```
else {
    toReturn.add(markdown.substring(openParen + 1, closeParen));
}
```
After updating that, the code is now correct for 567.

---

As for 520, that is still returning /uri. Because of the fact that there are no 
spaces in the text between the parentheses, it is being added to the list. To 
fix this issue, I simply need to add another nested if statement in the else if 
statement to ensure that the substring between the parentheses contains a period.

i.e.
```
if (markdown.substring(openParen + 1, closeParen).contains(".")) { 
}
```

