# **Lab Report 4 - MarkdownParseTest Snippets**

Today we are debugging!

[*Here*](https://github.com/heter13/markdown-parse) is my respository. 

[*This*](https://github.com/zfxd/markdown-parse) is the reviewed respository. 

The final set of links I decided would be the correct ones were:

```
<[url.com, google.com, google.com, ucsd.edu]>
```
```
<[a.com, b.com, example.com]>
```
```
<[https://www.twitter.com, https://ucsd-cse15l-w22.github.io/, 
https://cse.ucsd.edu/]>
```
In order to test these snippets, I created them as markdown files and added new
test cases to test them. I created a new ArrayList and added the links as 
necessary. Then I used the assertEquals method to test MarkdownParse after
calling it on the snippet files.

Here are the tests:
```
    @Test
    public void test2() throws IOException{
        Path fileName = Path.of("snippet1.md");
        System.out.println(fileName.toString());
	    String contents = Files.readString(fileName);
        ArrayList<String> links = MarkdownParse.getLinks(contents);   
        ArrayList<String> expected = new ArrayList<String>();
        expected.add("url.com");
        expected.add("google.com");
        expected.add("google.com");
        expected.add("ucsd.edu");
        assertEquals(expected, links);
    }
    @Test
    public void test3() throws IOException{
        Path fileName = Path.of("snippet2.md");
        System.out.println(fileName.toString());
	    String contents = Files.readString(fileName);
        ArrayList<String> links = MarkdownParse.getLinks(contents);   
        ArrayList<String> expected = new ArrayList<String>();
        expected.add("a.com");
        expected.add("b.com");
        expected.add("example.com");
        assertEquals(expected, links);
    }
    @Test
    public void test4() throws IOException{
        Path fileName = Path.of("snippet3.md");
        System.out.println(fileName.toString());
	    String contents = Files.readString(fileName);
        ArrayList<String> links = MarkdownParse.getLinks(contents);   
        ArrayList<String> expected = new ArrayList<String>();
        expected.add("https://www.twitter.com");
        expected.add("https://ucsd-cse15l-w22.github.io/");
        expected.add("https://cse.ucsd.edu/");
        assertEquals(expected, links);
    }
```
---
## Results
---
Unfortunately, neither implementation was able to correctly pass the tests. 

Here is the error message for my implementation:

![Failure](https://i.gyazo.com/9f42439fbd5528376bbfac11245b7051.png)

And here is the error message for the reviewed implementation:

![Failure](https://i.gyazo.com/7811a8e941b3513ce52c220f038980a3.png)

---
## Questions
---

- Do you think there is a small (<10 lines) code change that will make your 
program work for snippet 1 and all related cases that use inline code with 
backticks? If yes, describe the code change. 
If not, describe why it would be a more involved change.


Yes, I think that I could make a small code change to my code to make it work
properly for snippet 1. The only code change I would have to make would be to 
have MarkdownParse ignore the ' character. Since there is only one ' in the
link section, I could write an if statement that increments the currentIndex
by 1 whenever the string of currentIndex == '.

i.e

```
if (markdown.substring(openParen + 1, closeParen).contains(''')) {
    toReturn.add(markdown.substring(openParen + 2, closeParen));
}
```

- Do you think there is a small (<10 lines) code change that will make your 
program work for snippet 2 and all related cases that nest parentheses, 
brackets, and escaped brackets? If yes, describe the code change.
If not, describe why it would be a more involved change.

For starters, this question, along with the question for snippet 3, is somewhat 
up in the air because I got a StringIndexOutOfBoundsException although I could
not deduce why exactly that is since the currentIndex starts at 0 and when 
decremented, should be at -1 at the worst, not -2. However, I do believe that 
my code would work given the current state. If not, I think that a change to the
code made to ignore the parentheses if there is no text between them, or if 
there are parentheses between the parentheses would be a suitable fix.
i.e. 
```
if (markdown.substring(openParen + 1, closeParen) != "" ||
markdown.substring(openParen + 1, closeParen) != "()") {
    toReturn.add(markdown.substring(openParen + 1, closeParen));
}
```

- Do you think there is a small (<10 lines) code change that will make your 
program work for snippet 3 and all related cases that have newlines in brackets 
and parentheses? If yes, describe the code change. If not, describe why it 
would be a more involved change.

Yes, I think that snippet 3 would perhaps work if I simply remove the line that
ignores spaces in between the parentheses, or if I change it to increment the 
OpenParen until it hits a suitable link.

i.e.

```
- if (markdown.charAt(nextOpenBracket-1) != '!') {}

OR 

while (markdown.substring(openParen, openParen + 2) == " ") {
    openParen++;
}
```