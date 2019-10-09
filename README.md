# vs-kangaroo
Pollard, kangaroo method, solving discrete logarithm problem (DLP) using pseudorandom walks, c++.
Based on engine VanitySearch1.15

Runtime expected of 2w<sup>1/2</sup> group operations.

# Feature:

 - multicore
 - pollard method without same sequences

Expected in the future
 - gpu
 
 # Benchmark libs
Algo: 1T+3W with distinguished points,  expected of 2w<sup>1/2</sup> group operations

4core i7-6820, win7x64
```
1.1Mk/s
```

# Discussion
more info

https://bitcointalk.org/index.php?topic=5173445.msg52473992#msg52473992

https://bitcointalk.org/index.php?topic=5166284.msg52318676#msg52318676

# How pollard-kangaroo works, the Tame and Wild kangaroos, is a simple explanation.

Suppose there is pubkeyX, unknow privkeyX, but privkeyX is in range w=[L..U]. 
The keys have a property - if we increase pubkey by S, then its privkey will also increase by S. 
We start step-by-step to increase pubkeyX by S(i), keeping sumX(S(i)). This is a Wild kangaroo. 
We select a random privkeyT from range [L..U], compute pubkeyT. 
We start step-by-step to increment pubkeyT by S(i) while maintaining sumT(S(i)). This is a Tame kangaroo. 
The size of the jump S(i) is determined by the x coordinate of the current point, so if a Wild or Tame kangaroo lands on one point, their paths will merge. 
(we are concerned with pseudo random walks whose next step is determined by the current position) 
Thanks to the Birthday Paradox (Kruskal's card trick), their paths will one day meet. 
Knowing each traveled path (sumX and sumT), privkeyX is calculated. 
The number of jumps is approximately 2w<sup>1/2</sup> group operations, which is much less than a full search w. 

# Articles

base
https://andrea.corbellini.name/2015/05/17/elliptic-curve-cryptography-a-gentle-introduction/

hand translate to ru/ua (recommend instead translate.google)
https://habr.com/ru/post/335906/


- [1] Best of the best, all in 1, epic,  2012

Chapter 14. Factoring and Discrete Logarithms using Pseudorandom Walks 
https://www.math.auckland.ac.nz/~sgal018/crypto-book/ch14.pdf

- [2] with reference to old

J. M. Pollard, “Kangaroos, monopoly and discrete logarithms,” Journal of Cryptology, #13 (2000) 
https://web.northeastern.edu/seigen/11Magic/KruskalsCount/PollardKangarooMonopoly.pdf

(good dir web.northeastern.edu/seigen/11Magic/KruskalsCount/)

- [3] About parallelism problems

P. C. van Oorschot and M. J. Wiener, Parallel collision search with cryptanalytic applications, J. Cryptology, #12 (1999) 
https://people.scs.carleton.ca/~paulv/papers/JoC97.pdf

