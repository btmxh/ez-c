# 2. Variables

Before talking about variables, you should know how computer store data in memory.

You're probably familiar with binary numbers right? 0 is 0, 1 is 1, but 10 is 2 and 11 is 3, etc. This is how computer store data. A bunch of 0 and 1. However, a "unit" of storage is not just a 0 or 1 (or bit), it's a byte, which consists of 8 bits (in almost all platforms.

Using simple math, you can figure out a byte can store 2^8 = 256 different values. And using multiple bytes, the potential is infinite. For example, 4 bytes can store 256^4 = 4,294,967,296 values, 8 bytes can store 18,446,744,073,709,551,616 values.

And since the "unit" of storage is a byte, people want to use some kind of digit to store that, but since 256 digits is probably a nightmare to remember, so they reduced that to 16, they will use 2 digits for 1 byte. This is where hexadecimal come to play.

For example, the byte 0xC5 (0x is just a prefix) is 12 * 16 + 5 = 197 in base 10 (C is 12).

But people also want to do math with negative numbers. The most straight forward way to do it is using a bit for the sign, and all of the other 7 bits for the number value. Although its simplicity, this is not the best way to do thing.

Let's look at the byte 0xC5, it's 11000101, so it's signed value should be -1000101 (or some derivation), -69 in base 10. But as you can see, there is no visible connection between 197 and 69. The new way will solve this issue, it's called two's complement.

In the unsigned world, 0xC5 is 197. And in order to make this value signed, you subtract it to 256 if its first bit is 1, or keep the same value otherwise. So 0xC5 is -59. This is the interesting part, 197 and -59 is congruent mod 256, so their behavior in addition and subtraction is basically the same (in mod 256). Their representation in base 2 is also "similar", but you should see it for yourself.

That's the rule for storing integer. For floating-point numbers and text, the rule will be a little more complex, but you just need to understand this: basically everything on a computer is a bunch of bytes, a bunch of numbers ranging from 0 to 256 (or -128 to 127 in the signed world).

Let's look at something bigger. 4 bytes. A lot of you should already heard about 32-bit and 64-bit, and when you translate them to bytes, you got 4-byte and 8-byte. While a byte is a "unit of storage" for a computer, a computer likes to work with things based on 4 or 8 bytes (depending on your CPU, there are also 16-bit CPU but no one uses them anyways, or if you use them, you should look at a more specific tutorial about them) 

The reason is, well, 256 is quite a big number, but you've already seen a lot of bigger numbers in a computer, right? There are even numbers which have more than 256 digits (in base 10). This is why people like CPU to handle bigger number natively, so they invented 32-bit CPU, and then 64-bit CPU.

This is why, int, a data type to store 32 bit integer, is widely used. But what exactly is a data type though?

4 bytes. You can use it to store 4 8-bit integer (or bytes), 2 16-bit integer (or shorts), or 1 32-bit integer (or int). There are also 32-bit floats and stuff like that. Data type is a way to distinguish between them.

OK, after all of this, we can finally use variables in our program. Let's look at this simple C program.

```c
int main() {
  return (1 + 1) * (1 + 1);
}
```

Yes, the compiler will optimize and replace the expression after return with 4, but let's pretend the compiler is dumb and will make the program do all of the calculations. The expression consists of 2 additions and 1 multiplication. We also sees that the expression (1 + 1) is computed twice, so it would be best to store that value to somewhere else and do only 1 addition and 1 multiplication. Variables will help us achieve this.

First we need to declare a variable. We will need a place in memory to store our result to (1 + 1), so we asked the program for some memory by just calling:

```c
int x;
```

Also we will call our variable 'x', since you will need not just one variable in C, and you'll need to distinguish between them. Depends on where you put that line (inside or outside main() function), the memory for x will be in different places.

Next, you store the result of 1 + 1 to x:

```c
x = 1 + 1;
```

This line must be inside the main() function, since you're asking the computer to do stuff, and main() is where all of your directives are. And if you previously put the "int x;" line after main(), there will be an error, since the C compiler read your code line by line. When it read your "x = 1 + 1;" line, it will not know what x is. So you have to move your declaration of x before or inside the main() function

(Like this:
```c
int x;

int main() {
  x = 1 + 1;
}
```
)

Finally, the return statement. It should be
```c
return x * x;
```

And your final code should be:

```c
int x;

int main() {
  x = 1 + 1;
  return x * x;
}
```

or 

```c
int main() {
  int x;
  x = 1 + 1;
  return x * x;
}
```

There are still a lot of thing worth mentioning.

First, if you go for the second approach (declare x in main()), you can combine your first two lines to just
```c
int x = 1 + 1;
```

Second, you should go for the second approach, because you can do the thing I've just mention earlier, and you can't access x from anywhere else than your main() function. This will make stuff a lot easier to handle. (more restriction = better code, usually)

Third. We will talk about pointers. This is going to be long.

Since C is a low-level language, there is the concept of pointers. They are address for a block of memory. Let me explain.

Let's look at the previous program:

```c
int main() {
  int x = 1 + 1;
  return x * x;
}
```

On the return line, what do you think the CPU will do? It'll load the value from x, multiply that value with itself, and then return it to the OS or something, right? But where exactly would it load the value from?

The answer to that question is the pointer of x, written as &x in C. This is where x is stored. (You will also ask yourself, where is &x stored? Quick answer, on the stack. But
