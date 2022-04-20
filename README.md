# Solving Double Execution of Java's `paint()` Method by Counting Down to the Heat Death of the Universe

ArnoldC implementation of the heat death algorithm proposed in `"Solving Double Execution of Java's paint() Method by Counting Down to the Heat Death of the Universe"`, published for [SIGBOVIK 2022](http://sigbovik.org/2022/).

The published paper is available in the online proceedings: <http://sigbovik.org/2022/proceedings.pdf>, pp. 111-137.

Other less interesting implementations were written for Ruby (section 3.9), Go (3.12), Scratch (3.14), and OCAML (3.15).

## Explanation

> Extracted from the published paper, section 3.18 of SIGBOVIK 2022 proceedings p.120.

ArnoldC is an imperative JVM-bytecode assembly language in which instructions and basic keywords are replaced with one-liners from different Arnold Schwarzenegger movies. The language, having its syntax comprised of well-known phrases, is an ideal choice for applications developed by fans and movie-goers. Promisingly, its code is also readable by almost any individual, with or without any formal programming knowledge, as it only requires proficiency in English and Schwarzenegger mannerisms. The language, compiling directly to JVM bytecode, is also able to run on any platform without recompilation. Tragically, ArnoldC has no built-in support for bignums, timing functionality, nor any way to make system calls. As such, traditional methods like those presented in other languages [looping, system calls, etc] are provably impossible.

Building on the work done by Lambert and Power (1), however, we can approximate a solution using the execution time of a known bytecode. As shown in their paper, we know with confidence that any used bytecode time is platform-independent (in every regard except processor speed, for which we account during usage), making it an useful drop-in as a base unit of elapsing time in a general-purpose solution. From the 137 timed bytecodes, we pick integer division (`idiv`) due to its comparatively (by an order of magnitude) longer execution time of `3.449739E-8` seconds vs. all other used operations; thus, our implementation can delay for longer increments and be more efficient. Floating point conversions (`d2i` and `f2i`) take longer, but cannot be used as ArnoldC only supports 16-bit signed integers.

Combining this novel unit of time with the recursive approach demonstrated in B and the common looping approach, and knowing that our selected bytecode consumes a magnitude more time than the other programmatic instructions, we can successfully implement an ArnoldC program that will amortizedly delay for our desired time. To achieve heat death, we must recurse the number of times it takes to reach `10^100` years, which assuming a time unit of `3.449739E-8` seconds, equates to `10^100∗(31536000 / 3.449739E−8) ≈ 10116` iterations. The implementation provided achieves this through deep recursion, where each recurse recurses 10 times.

Lambert and Power calculated the used bytecode instruction time using a ≈1GHz dual core Intel Pentium III. To account for processors operating outside of the 1-10GHz range, the programmer can simply decrement or increment the magnitude of iterations for each magnitude difference in processor speeds (116 ± 1n).

> 1. Lambert, J. M., J. F. Power, _Platform Independent Timing of Java Virtual Machine Bytecode Instructions_, Electronic Notes in Theoretical Computer Science. **220** (2008), pp. 97–113.

## Execution

```sh
# download ArnoldC compiler and compile
$ wget http://lhartikk.github.io/ArnoldC.jar
$ java -jar ArnoldC.jar heatdeath.arnoldc

# run
$ java heatdeath
```

## License

MIT License

Copyright (c) 2022 Elias Gabriel

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to
deal in the Software without restriction, including without limitation the
rights to use, copy, modify, merge, publish, distribute, sublicense, and/or
sell copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
DEALINGS IN THE SOFTWARE.