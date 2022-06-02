[Return to home page](https://crustaceanking.github.io/cse15l-lab-reports/Lab-reports.html)

# Lab Report 5

choose two differing tests, compare the code, see which is right/wrong and explain

## How I found the Test

>vimdiff, bash for loop, search manually, other way?

## Link to test files

Test 14: [14](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/14.md)

Test 201: [201](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/201.md)

# Test 1: File 14 

Test Number 14

[Test File](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/14.md)

## Comparison screenshot

![Image](Lab5Comp14.png)

As we can see, the difference on test 14 between my code and the given code is that my code did not pick up "/foo" and a valid link, whereas the given code did

## Expected Output

![Image](Lab5Test14Img.png)

**What should it produce?**

As we see from the image, the only link that the markdown picked up was what was comtained in "not a link", which happened to be /foo. So while technically /foo itself if not a link, makrdown believes it to be a valid link, therefore it should be picked up by the parser, and the expected output should be  "[/foo]"

## Which Test is Correct?

Simply based on Markdown rules, the given test was correct, and my test was incorrect. Comparing to the image above, the only link returned should have been "/foo", which the given code returned but my code not. Therefore simply by markdown standards, the given code test is correct

## For Incorrect Implementation, describe bug

# Test 2: File 201

Test Number 201

[Test File](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/201.md)

## Comparison screenshot

![Image](Lab5Comp201.png)

As we can see, the code outputs differ here as my code did not pcik up "baz" as a valid link, whereas the given code did

## Expected Output

![Image](Lab5Test201Img.png)

**What should it produce?**

Again with the last test, we see that markdown sees the "[foo]" followed by a colon, followed by (baz) as a valid link, and picks up the link baz with a title foo. Even though as with the last test "baz" itself is not a valid link, and if we click on it we get a "404 page not found", because markdown think's it is a link the expected output should pick this up and therefore be "[baz]"

## Which Test is Correct?

Simply based on Markdown rules, the given test was correct, and my test was incorrect. Comparing to the image above, the only link returned should have been "baz", which the given code returned but my code not. Therefore simply by markdown standards, the given code test is correct

## For Incorrect Implementation, describe bug
