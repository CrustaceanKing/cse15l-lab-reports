3 Changes made to code

First change:
[first](https://github.com/CrustaceanKing/markdown-parser/commit/a2cd687791e507bf66f70c6e0e8f6c72a50139e6)

Test file;

Symptims of failure;
Our of memory error when code tries to complie, infinite loops causes code to crash

for the first error, the code would infinitely loop because if there were no more brackets or parenthesis, the code would assign the instance variables a value of -1.
Because there was no check if they were -1, it would infinitely loop and eventually cause an out of memory error. This was fixed by adding a break statement when the code did assign instance variables a value of -1, so that it never loops.

Second change:
[second](https://github.com/CrustaceanKing/markdown-parser/commit/d2e36736316762680eaaac9b63283202853add0d)

Test file;

Symptoms of failure;
If link had parenthesis in it, would cause the code to end the link early

What I did here was check to make sure that the last parenthesis comes after the .com statement, therefore it wouldn't end early. Unfortunately, while this did work for the .com exception, it didn't work for any others.
