# **Lab Report 2 - Code Changes**

   <br>

## **First Code Change**
---

The first code change I have chosen is of the MarkdownParse file.

The code change can be found [*here*](https://github.com/heter13/markdown-parse/commit/b7410fae4597c74467f225013d7f2c7bb132eb10).

The code breaking file can be found [*here*](https://github.com/heter13/markdown-parse/commit/97fa0964b774c474e8a7ad4c9ac700f4747e9cc3#diff-e6c5de13727de2c05c1f603e3e6dce00abfea79591bf2480caa31e15c0f05311).

This is the output message that shows the failure of the code.

![FailImage](https://i.gyazo.com/ee09db7fffe7709cf1974bf8827d6cc1.png)

Essentially, the MarkdownParse code worked, but it also worked for image files. We did not want to return the links for images, so the newtest-file broke the code. This was counteracted by including an if statement that checks if the input is an image link by checking if it is preceded by the '!' character.

---

## **Second Code Change**

---

The second code change once again comes from the MarkdownParse file and test file.

The code change can be found [*here*](https://github.com/heter13/markdown-parse/commit/67b0004a318b81850f1a1007bcdd872477c8c560#diff-c703a0ec03474d601c6bf846740b293e0538bccf38d5f677a302457479e9c652).

The code breaking file can be found [*here*](https://github.com/heter13/markdown-parse/commit/7237331b1c494ac76782b1503dd55a8f34e8a830#diff-e6c5de13727de2c05c1f603e3e6dce00abfea79591bf2480caa31e15c0f05311).

This is the output message that shows the failure of the code.

```
PS C:\Users\heter\Documents\GitHub\markdown-parse> java MarkdownParse newtest-file.md
Exception in thread "main" java.lang.StringIndexOutOfBoundsException: String index out of range: -1
        at java.base/java.lang.StringLatin1.charAt(StringLatin1.java:48)
        at java.base/java.lang.String.charAt(String.java:712)
        at MarkdownParse.getLinks(MarkdownParse.java:19)
        at MarkdownParse.main(MarkdownParse.java:30)
```

The previous code change worked to remove images, but it was contingent on there being a heading or something in the beginning of the code. When there is a link in the first line of a markdown file, the index is out of bounds as it is at 0 and the loop is checking for the index below that (-1). This returns a StringIndexOutOfBoundsException. This was fixed by adding another if statement to check if all open brackets are at index > 0. If they are, then it will return all links. If not, then it can be skipped since if the open bracket is an index 0, it will be a link.

---

## **Third Code Change**

---

The third code change also again comes from the MarkdownParse file and test file.

The code change can be found [*here*](https://github.com/heter13/markdown-parse/commit/5675aab158f4259f75460be93c18b667507836af#diff-c703a0ec03474d601c6bf846740b293e0538bccf38d5f677a302457479e9c652).

The code breaking file can be found [*here*](https://github.com/heter13/markdown-parse/commit/5e02beedf9c2ba007102dc0018e2b26091afece4#diff-d902b3a6dba925548b7ea18ffb80dd0c28f1bc45f1d738a5da414273711a4409).

This is the output message that shows the failure of the code.

```
PS C:\Users\heter\Documents\GitHub\markdown-parse> java MarkdownParse newtest-file.md
[are we sure]
```

The issue with the code this time around is that it will add whatever is in the parentheses even if they are not links. This is because there is no check on if the link is valid, only if there is not a ! in the front. To fix this, I added a check with contains() to make sure there is no spaces in the parentheses as it should be a link. If there is, it will not be returned. Since the other link contains the ! for an image link, it is also not returned.