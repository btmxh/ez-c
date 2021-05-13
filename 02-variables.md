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

Let's look at something bigger. 4 bytes. A lot of you should already heard about 32-bit and 64-bit, and when you translate them to bytes, you got 4-bytes and 8-bytes. While a byte is a "unit of storage" for a computer, a computer likes to work with things based on 4 or 8 bytes (depending on your CPU, there are also 16-bit CPU but no one uses them anyways, or if you use them, you should look at a more specific tutorial about them) 

The reason is, well, 256 is quite a big number, but you've already seen a lot of bigger numbers in a computer, right? There are even numbers which have more than 256 digits (in base 10). This is why 
