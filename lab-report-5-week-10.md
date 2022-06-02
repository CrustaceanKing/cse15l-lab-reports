[Return to home page](https://crustaceanking.github.io/cse15l-lab-reports/Lab-reports.html)

# Lab Report 5

choose two differing tests, compare the code, see which is right/wrong and explain

**NOTE FOR GRADER:**
In the Lab 5 write up, it mentions "The tests with different answers should correspond to different bugs – that is, you couldn’t easily fix both with one code change." **HOWEVER**: I have gone through like 19 tests at this point that were different, and they all come down to this same bug, which happens because my version of markdown parser checks if the links are valid links, whereas the markdown language does not. 

Here is a link to my [Piazza Post](https://canvas.ucsd.edu/courses/35489/external_tools/3269)

If link doesn't work it is @805

Because of this, I decided to check two tests anyways, and even though they are likely caused by the same bug, for the second one I described a different bug that may also have influenced the results and cases when it would actually fail. Please understand this was about the greatest extent I could do, thanks.


### How I found the Test Files to Compare

How I went about finding the test files to compare was first for each repository containing the different markdown tests, I added a `script.sh`, which compiled the markdown parser on all 1000+ test files, then I ran `bash script.sh` and added the result to a file called `results.txt` (command line would be " `time bash script.sh > results.txt` ". This file would contain what the markdown would compile for each specific test file, for all test files (which was over 1000!)

Now that I had done this for each repository, meaning I had two different results.txt, each having the 1000+ files compiled on the specific repositories version of the markdown parser, I used vimdiff to compare them.

The command was: `vimdiff my-markdown-parser/results.txt cse15lsp22-markdown-parser/results.txt`

This allowed me to compare them side by side and see any differences. Two main ones I noticed were test 14, and test 201, so I will be looking at those


### Link to Test Files Used

Test 14: [14](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/14.md)

Test 201: [201](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/201.md)

# Test 1: File 14 

Test Number 14

[Test File](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/14.md)

### Comparison Screenshot

![Image](Lab5Comp14.png)

As we can see, the difference on test 14 between my code and the given code is that my code did not pick up "/foo" and a valid link, whereas the given code did

### Expected Output

![Image](Lab5Test14Img.png)

**What Should it Produce?**

As we see from the image, the only link that the markdown picked up was what was comtained in "not a link", which happened to be /foo. So while technically /foo itself if not a link, makrdown believes it to be a valid link, therefore it should be picked up by the parser, and the expected output should be  "[/foo]"

### Which Test is Correct?

Simply based on Markdown rules, the given test was correct, and my test was incorrect. Comparing to the image above, the only link returned should have been "/foo", which the given code returned but my code not. Therefore simply by markdown standards, the given code test is correct

### For Incorrect Implementation, Describe Bug

Ironcially, the reason my code did not work is because it is more correct than markdown itself, which sounds cocky but let me explain. In my code, as seen below, markParse2 (my markdown file) has a check to see if the link contains a "." character, and if it doesn't skip this link.
![Image](Lab5RedoTest1.png)
This is because in my mind a valid link would have to include some type of domain, such as .org, .edu, .gov, etc., which all have a "." seperating the domain from the rest of the link, therefore any links not containing the character "." were invalid, which for the most part is true! As we see with /foo, when we click on it we get a "404 Page Not Found"
![Image](Lab5Test14-404.png)
However, while this is *accurate*, it fails to consider that eventhough */foo is not a valid link*, **the markdown langauge will still pick it up as a valid link**. So for this to be a 100% accurate **markdown parser**, my code should have picked up the link, which is an easy fix as all I would need to do is delete the highlighted line above. Without a check of the ".", this link should've been picked up.

# Test 2: File 201

Test Number 201

[Test File](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/201.md)

### Comparison Screenshot

![Image](Lab5Comp201.png)

As we can see, the code outputs differ here as my code did not pcik up "baz" as a valid link, whereas the given code did

### Expected Output

![Image](Lab5Test201Img.png)

**What Should it Produce?**

Again with the last test, we see that markdown sees the "[foo]" followed by a colon, followed by (baz) as a valid link, and picks up the link baz with a title foo. Even though as with the last test "baz" itself is not a valid link, and if we click on it we get a "404 page not found", because markdown think's it is a link the expected output should pick this up and therefore be "[baz]"

### Which Test is Correct?

Simply based on Markdown rules, the given test was correct, and my test was incorrect. Comparing to the image above, the only link returned should have been "baz", which the given code returned but my code not. Therefore simply by markdown standards, the given code test is correct

### For Incorrect Implementation, Describe Bug

Again, the reason my code did not pick up this link was because it's too accurate: It does not include links that do not contain a domain, as checked by the existance of a ".". 
**However**, because of the rule of not talking about the same bug, I will discuss another bug which may have called this issue. In my code, if the end bracket ] is not directly before the open parenthesis (, the code will not include this link. This may actually also be why the code did not pick up on the baz, as there was a : and a space character seperating the two, so my code, seeing this, would not include this link, even though as we see above markdown itself picks this up as a valid link. Here is an image of the line in my code that would case this error
![Image](Lab5RedoTest2.png)
Again, even though this is not the expected output, my output is technically, correct: "baz" is not a valid link as seen below (Also note how it's Obi Wan on Tatooine, probably because of Kenobi, which is 8/10 ngl, but I just found that funny). However, if this was a valid link, my output would be incorrect, as it would miss this link entirely due to the fact that there was a space between the end bracket and the open parenthesis of the link.
![Image](Lab5404201.png)
Unfortuantley for my code, markdown both recignizes baz as a link and also recognizes a space between the brackets arguemnt and the parenthesis arguemnt as still valid for links. A quick fix for this bug may be to remove those lines all togther, however some further algorithm may need to be implemented as links cannot exceed a newline character, so further testing on the exact distance markdown allows between links and brackets would be necessary to find out what would accurately fix this issue
