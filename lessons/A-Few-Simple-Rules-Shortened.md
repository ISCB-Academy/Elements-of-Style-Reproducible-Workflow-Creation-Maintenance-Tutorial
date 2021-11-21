<p>
</p>
<br/><br/>


# A Few Simple Rules - Shortened Editions

## Disclaimer

The views expressed in this course represent the views of Anne Deslattes Mays, PhD and do not represent the views of NICHD, NIH or the United States Government.

**`In what follows - is my development of a practice that enables workflow and platform independence facilitating reproducibility.`**

## Learning from those who have walked the journey

[Elements of Programming Style](https://en.wikipedia.org/wiki/The_Elements_of_Programming_Style)
[B. W. Kernighan and P. J. Plauger, The Elements of Programming Style 2nd Edition, McGraw Hill, New York, 1978. ISBN 0-07-034207-5](https://www.gettextbooks.com/isbn/9780070342071/)

[Quotes by P. J. Plauger](https://softwarequotes.com/author/p--j--plauger)

The year was 1919, the first World War was at its close and a student, E. B. White, took a course, English 8, taught by William Strunk Jr.  The course featured a required textbook, a slim volume called **The Elements of Style**.  The durability of this slim book informed the development of the book, **The Elements of Programming Style** by Kernigan and Plauger,  whose lessons we adapt here in this course. Showing again the durability of the approach of beginning with philosophy as one approaches their work and use of programs and structure to achieve their work.

So with this nod to E.B. White, William Strunk, Jr, Brian Kernigan and Plauger, we begin with our own Lessons and Pithy Phrases.

### Lessons **`Translated to the Workflow/Containerized Process`** (Truncated Pithy Phrases)

Where I have made modifications to these `Pithy Phrases` to the map to what we are teaching here **`will be in bolded and emphasized`**

Its lessons are summarized at the end of each section in pithy maxims, such as "Let the machine do the dirty work":

1. Write clearly – don't be too clever. **`timeless`**
2. Say what you mean, simply and directly. **`timeless`**
3. Use **`containerized processes`** (in a way similar to library functions) whenever feasible.
5. Write clearly – don't sacrifice clarity for efficiency. **`timeless`**
6. Let the machine do the dirty work. **`timeless`**
7. Replace repetitive expressions by calls to common functions. **`timeless - when you start to see yourself do this - replace with a single function`**
9  Choose variable names that won't be confused. **`timeless`**
11. If a logical expression is hard to understand, try transforming it. **`timeless`**
13. Write first in easy-to-understand pseudo language; then translate into whatever language you have to use. **`timeless`**
14. Modularize. Use procedures and functions. **`and containerize - use GitHub Actions to build, test and keep up-to-date`**
17. Write and test a big program in small pieces. **`timeless this can be done by the use of these tested, dockerized processes`**
19. Test input for plausibility and validity. **`timeless - make sure you understand the source of your data`**
25. Make input easy to proofread. **`timeless`**
29. Use debugging compilers. **`timeless this is different with workflow languages - you can test each of the steps in the workflow verifying inputs, outputs and processes - dockerizing, testing `**
30. Watch out for off-by-one errors. **`timeless`**
25. Check some answers by hand. **`timeless`**
29. Make it right before you make it faster. **`timeless for everything`**
30. Make it fail-safe before you make it faster. **`timeless`**
31. Make it clear before you make it faster. **`timeless`**
32. Don't sacrifice clarity for small gains in efficiency. **`timeless`**
33. Let your compiler do the simple optimizations. **`again, for our world of platforms, let your platform help you - Platforms as a Service, such as CAVATICA by Seven Bridges, CloudOS by Lifebit, DNANexus Apollo by DNANexus`**. 
34. Don't strain to re-use code; reorganize instead. **`timeless the more you perform a task, the simpler you see how to get it done, exploit that simplicity and rewrite`**
35. Make sure special cases are truly special. **`timeless`**
36. Keep it simple to make it faster. **`timeless`**
37. Don't diddle code to make it faster – find a better algorithm. **`timeless find another Bioinformatics algorithm, collaborate, give attribution and expand your reach`**
38. Instrument your programs. Measure before making efficiency changes. **`timeless - this means if you introduce changes - are they appropriate`**
39. Make sure comments and code agree. **`timeless`**
40. Don't just echo the code with comments – make every comment count. **`timeless`**
41. Don't comment bad code – rewrite it. **`timeless`**
42. Use variable names that mean something. **`timeless`**
44. Format a program to help the reader understand it.**`timeless`**
45. Document your data layouts. **`timeless`**
46. Don't over-comment. **`timeless`**

## Other useful and informative points

[Juptyer Notebooks to Fix the Reproducibility Crisis](https://medium.com/@CH_maria_CH/fixing-the-reproducibility-crisis-in-science-lifebit-cloudos-meets-jupyter-6939a7e9bc77)

