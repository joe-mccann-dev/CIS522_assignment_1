# Assignment 1

- **Name**: Joseph McCann
- **Course**: CIS 522
- **Topic**: Introduction and Algorithm Analysis
- **Due Date**: 2024-09-17

## Exercises

### Ch 1 Exercise 4. 

#### Present an algorithm to solve the hospital-student matching problem

```
Initially all hospitals h ∈ H have available residency positions and all medical students s ∈ S are seeking residency positions.
While there is a hospital h with available residency positions
  Choose such a hospital h
  for each student in h's preference list not already offered a position
    Let s be the highest-ranked student in h's preference list to which h has not yet offered a residency
    If s is free then
      s tentatively accepts h's offer and joins as resident
    Else s agreed to position at other hospital h'
      If s prefers h' to h then
        position at h remains available
      Else s prefers h to h'
        s accepts position at h
        position at h' becomes available
      Endif
    Endif
  Endfor
Endwhile

return the set S of hospitals matched with residents     
```
#### Analyze the time complexity of this algorithm

If each iteration of the above algorithm is implemented in constant time, then the algorithm will have a time complexity of n<sup>2</sup>. This is because the outer loop must iterate over _n_ hospitals. Then for each hospital _h_, the algorithm iterates _m_ times for each student in its preference list. For any hospital with an unfilled residency due to the undoing of a tentative match, the outer loop will have to repeat a constant _k_ amount of times. Therefore expanded time complexity is (n + k) * m => n * m => n<sup>2</sup>

#### Show this algorithm does find a stable assignment by proving the two types of instabilities cannot exist in the solution found by this algorithm

The first type of instability the text identifies, given students _s_ and _s'_ and a hospital h, is when a student _s_ is assigned to _h_ but _h_ prefers _s'_. Meanwhile _s'_ isn't assigned to a hospital at all. The algorithm above ensures this instability never occurs because if the hospital _h_ has done its job and assembled a preference list, then s' will be ahead of s in the preference list of hospital _h_. The following pseudo code ensures this instability never happens:

```
for each student in h's preference list not already offered a position
    Let s be the highest-ranked student in h's preference list to which h has not yet offered a residency
    If s is free then
      s tentatively accepts h's offer and joins as resident
```

The second type of instability the text mentions is the following:

- _s_ is assigned to _h_, and
- _s'_ is assigned to _h'_, and
- _h_ prefers _s'_ to _s_, and
- _s'_ prefers _h_ to _h'_.

To summarize the above scenario, neither student _s'_ nor hospital _h_ gets their preferences honored. However, in the algorithm above, this instability is avoided. Imagine the algorithm iterates on hospital _h'_ first and so _h'_  gets to select their preferred student _s'_ first, before hospital _h_ and _s'_ is free. _s'_ then tentatively accepts the offer from _h'_. Now when the algorithm iterates on hospital _h_, _s'_ is given the opportunity to "jump ship" to _h_ because that is their preference (see second else block).

### Ch 2 Exercise 2

#### **2(a)** n<sup>2</sup>

There are 3600 seconds in an hour. Multiply 3600 sec/hr by 10 Billion operations/sec to get 3.6 * 10<sup>13</sup> ops/sec. Solve for n.

n<sup>2</sup> = (1 * 10<sup>10</sup>) * (3.6 * 10<sup>3</sup>) = 3.6 * 10<sup>13</sup>.

n = sqrt(3.6 * 10<sup>13</sup>) = 6,000,000

#### **2(b)** n<sup>3</sup>

Repeat the same process as above since the operations per second remains the same, we are simply solving for n again but this time taking cube root. Using my TI-84 calculator gives the following max input size that can be processed in one hour for a cubic function given 10<sup>10</sup> operations/second.

n = cube_root(3.6 * 10<sup>13</sup>) = 33019.27

#### **2(c)** 100n<sup>2</sup>

Here we can simply divide the answer found in part (a) by 100 before taking the square root to get:

n<sup>2</sup> = 3.6 * 10<sup>13</sup> / 100

n = sqrt(3.6 * 10<sup>11</sup>) = 600,000

#### **2(e)** 2<sup>n</sup>

Apply the same process to solve for n:

2<sup>n</sup> = (1 * 10<sup>10</sup>) * (3.6 * 10<sup>3</sup>) = 3.6 * 10<sup>13</sup>

log(2<sup>n</sup>) = log(3.6 * 10<sup>13</sup>)

n * log(2) = log(3.6 * 10<sup>13</sup>)

n = log(3.6 * 10<sup>13</sup>) / log(2) = 45.03

#### **2(f)** 2<sup>2<sup>n</sup></sup>

2<sup>2<sup>n</sup></sup> = (1 * 10<sup>10</sup>) * (3.6 * 10<sup>3</sup>) = 3.6 * 10<sup>13</sup>

2<sup>n</sup> * log(2) = log(3.6 * 10<sup>13</sup>)

....

log(2<sup>n</sup>) = log( log(3.6 * 10<sup>13</sup>) / log(2) )

...

n = ( log( log(3.6 * 10<sup>13</sup>) / log(2) ) ) / log(2)

n = 5.49

### Ch 2 Exercise 3

The function with the fastest growth rate will have the worst performance as _n_ approaches infinity. Likewise, the function with the slowest growth rate will have the best performance as _n_ approaches larger and larger values. To sort in ascending order, we start with the fastest performing algorithms (slow growth rate) and ascend the list to the slowest performing algorithms (fast growth rate). I plotted the graph on desmos here: [desmos graph](https://www.desmos.com/calculator/whayhrjjnt) 

1. f2(n) = sqrt(2n)
    - grows slower than linear time, we can ignore the constant 2
2. f3(n) = n + 10
    - linear time, the 10 is ignored
3. f1(n) = n<sup>2.5</sup>
    - grows slightly faster than quadratic time
4. f6(n) = n<sup>2</sup> * log(n)
    - because we are multiplying by an 'n', even though it's a log, it still grows faster than n<sup>2.5</sup>
5. f4(n) = 10<sup>n</sup>
    - exponential function, this grows much faster than a polynomial function.
6. f5(n) = 100<sup>n</sup>
    - another exponential function, 100x grows faster than 10x

### Ch 2 Exercise 4

All functions with n in the exponent except for 2<sup>sqrt(log n)</sup> will take up the bottom half. Here is my desmos graph for this exercise: [desmos graph 2](https://www.desmos.com/calculator/kjmlmrhxlh) 

1. 2<sup>sqrt(log n)</sup>
    - This function grows very slowly because it is raising the constant 2 to a very slow growing number. Sqrt function cuts down the impact of n being in the exponent, and then the log cuts it down even more.
2. n log n
    - This function grows faster than linear time but more slowly than quadratic time
3. n<sup>4/3</sup>
    - This function is closer to quadratic than linear in behavior
4. n(log n)<sup>3</sup>
5. 2<sup>n</sup>
    - Exponential function
6. 2<sup>n<sup>2</sup></sup>
    - A more quickly growing exponential function
7. 2<sup>2<sup>n</sup></sup>
    - An even more quickly growing exponential function