---
tags:
  - module
lecture_count: "1"
current_lecture: "1"
length: 1hr 16min
status: Ongoing
course_link: "[[COMP 2160 - Programming Practices]]"
link: https://www.youtube.com/watch?v=ygPgi5koLtU&list=PLGqzRfI3gmje2f9SN2OBtfgb3bqnVkzg1&index=3
module_number: 3
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [ ] Compare and contrast C and Java with a simple program
- [ ] Standard I/O
- [ ] Variables / Comparisons
- [ ] Loops
```

- The `switch` statement is the only time you should use the `break` keyword
- Use `while` loops for conditional logic and `for` loops for changing / iterating over each item
	- Eg. Search for index -> `while`
- `void` parameter in the main method -> no parameters

We'll be converting a familiar language (`Java`) to `C` to quickly familiarize ourselves with the syntax differences.

Consider the following Java program:

```java
import java.io.InputStreamReader;
import java.io.BufferedReader;
import java.io.IOException;

public class tolower
{
  // 
  public static void main(String args[])
  {
    int documentCharacter;
    InputStreamReader inputFile;
    BufferedReader stdin;

    // read the document 1 character at a time
    try
    {
      inputFile = new InputStreamReader(System.in);
      stdin = new BufferedReader(inputFile);

	  // get the input
      documentCharacter = stdin.read();

      // until no input
      while (documentCharacter > 0)
      {
        System.out.print(Character.toLowerCase((char)documentCharacter));

        documentCharacter = stdin.read();
      }

      // done
      stdin.close();
    }
    catch (IOException e)
    {
      System.out.print("IOException: " + e.toString());
    }
  }
}
```


```c
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h> // tolower

int main(void)
{
  int documentCharacter;

  // try block
  // C does not have exceptions

  // readers
  // C does not have readers

  // same as BufferedReader.read() in java
  documentCharacter = getchar();

  // java -> boolean type
  // c -> this is an integer, 1 or 0 (true or false)
  while (documentCharacter > 0)
  {
    // print either putchar or printf
    printf("%c", tolower(documentCharacter));

    documentCharacter = getchar();
  }

  return EXIT_SUCCESS;
}
```

---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
