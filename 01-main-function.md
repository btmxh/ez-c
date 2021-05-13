# 1. main() function

A lot of people start their C journey with this famous "Hello, World" program:

```c
#include <stdio.h>

int main() {
  printf("Hello, World!");
  return 0;
}
```

There are already a lot of things happening here like the C preprocessing directives, functions, string, etc. This is why we will take a different approach to it by looking at just the main() function only.

So what is a main() function?

To answer that, you need to ask yourself, what does a program do? Do all sort of stuff, right? Yes. The main() function is where you put the directives for a program to do.

Let me give you an example: (this is not a proper C program)

```c
int main() {
  CODE_THAT_MAKE_THIS_PROGRAM_PRINT_HELLO_WORLD;
  CODE_THAT_MAKE_THIS_PROGRAM_PRINT_HELLO_WORLD;
  CODE_THAT_MAKE_THIS_PROGRAM_PRINT_HELLO_WORLD;
}
```

If CODE_THAT_MAKE_THIS_PROGRAM_PRINT_HELLO_WORLD does its thing (which is 'make this program print "HELLO_WORLD"'), this program should print "HELLO_WORLD" three times.

But why are there some weird stuff like 'int', a pair of parentheses and brackets, also the semicolons too?

Let's look at them one by one.

First, you need to know that the C compiler (basically the program that make programs based on C code) doesn't care about newlines. You can put this input:
```c
int main() { CODE_THAT_MAKE_THIS_PROGRAM_PRINT_HELLO_WORLD; CODE_THAT_MAKE_THIS_PROGRAM_PRINT_HELLO_WORLD; CODE_THAT_MAKE_THIS_PROGRAM_PRINT_HELLO_WORLD; }
```
and you should get the same output.

If there are no semicolons, the code will be:
```c
int main() { CODE_THAT_MAKE_THIS_PROGRAM_PRINT_HELLO_WORLD CODE_THAT_MAKE_THIS_PROGRAM_PRINT_HELLO_WORLD CODE_THAT_MAKE_THIS_PROGRAM_PRINT_HELLO_WORLD }
```
the compiler would not know what to print, something like "HELLO_WORLD CODE_THAT_MAKE_THIS_PROGRAM_PRINT_HELLO_WORLD CODE_THAT_MAKE_THIS_PROGRAM_PRINT_HELLO_WORLD". Yes this is not a proper C program, but in C, the similar thing will happen without semicolons, so you need them to separate your directives.

The next thing, the bracket pair. This is used to separate code inside main() function with code outside it. Yeah, this is kinda self-explanatory.

Third, the parentheses pair. We will leave it for now (go to the function chapter for the reason).

Finally, the int keyword. We will talk about it using this example.

```c
int main() {
  return 0;
}
```

A proper main() function should have a line: return *something*;  
*something* here is usually a number, or more specific, an INTeger. Did you see where the 'int' come from? Basically, this is the return code for our program. If it's 0, the OS sees this number and said "Oh, this program exited successfully". But if it's not, the OS will know that there is something wrong with this program, and depends on your OS, maybe it will throw a huge error onto your screen like "App ... crashed" (Windows doesn't do this though, it uses some more advanced method for checking for error).

Another convenient thing is that not only number can be put to *something*, but you can put some complex expressions as well.

```c
int main() {
  return 3 * 4 - 12;
}
```

Since 3 * 4 - 12 is 0, this will have the same effect as return 0

