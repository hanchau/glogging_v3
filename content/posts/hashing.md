 +++
author = "hanchau"
title = "Hashing"
date = "2020-05-10"
description = "Hashing, A popular choice across all fields of CS"
tags = [
    "Hashing",
    "Hash Functions",
    "Hash Table",
    "Python Dictionaries"
    ]
categories = [
    "Concept",
]
+++

## A Brief History.

Arousal of an idea parallelly at multiple places is indicative of its need in the ecosystem. Like many ideas in Computer Science, Hashing was also introduced independently by different scientists. According to [Wikipedia](https://en.wikipedia.org/wiki/Hash_table#History), In 1953, At IBM, one computer scientist named Hans Pete Luhn wrote an internal memorandum that used Hashing (with Chaining), and about the same time, a group of scientists Gene Amdahl, Elaine M. McGraw, Nathaniel Rochester, and Arthur Samuel wrote a program using Hashing. After that, there has been a lot of work/research around Hashing. I can't think of a computer science field where we don't use Hashing. So Let's move right on to the concept.

## Concepts/Definitions.

### Hash Function
The definition of a Hash Function is pretty straight forward -
A Hash Function is a function {{< katex >}}\hat h{{< /katex >}} which maps a set of an arbitrary number of elements to a set of a fixed number of elements i.e.
{{< hint info >}}
{{< katex display >}} f(\xi) = \hat h(\xi) {{< /katex >}} s.t.
{{< katex >}} [\xi] = \infty {{< /katex >}} and
{{< katex >}} [\hat h(\xi)] = m {{< /katex >}} where
{{< katex >}} m {{< /katex >}} is also called number of buckets.
Usually
{{< katex >}} \hat h(x) \in [0, m-1]{{< /katex >}}.

{{< /hint >}}

### Collisions
We say, A Collision has happened if, for any two inputs to the hash function
{{< katex >}}\hat h{{< /katex >}}, we get the same output i.e.
{{< hint info >}}
{{< katex display >}} \exists x_1, x_2 \in \xi,  x_1 \neq x_2, but {{< /katex >}}
{{< katex display >}} \hat h(x_1) = \hat h(x_2) {{< /katex >}}
{{< /hint >}}

### Hash Table/ Hash Map
As the name suggests, A Hash Table is a table made up of two primary fields, key, and value. The field 'key' stores the keys from the set
{{< katex >}}\xi{{< /katex >}}
and the field 'value' stores the address of the corresponding value in the memory.



#### The High Level Store.

key     |   value
--------|-------
  dog   |   bark
  cat   |   meow
 snake  |   hiss
  lion  |   roar
  me    |   arrae


#### The Low Level Diagram.
{{< mermaid >}}

graph TB
    lion --> 4 --> B
    snake --> 7 --> A
    subgraph keys
    dog --> cat --> lion --> snake --> me
    end
    subgraph hash
    0 --> 1 --> 4 -->7 -->8
    end
    subgraph memory
    A["0X123, hiss"] --> B["0X234, roar"] --> C["0X324, bark"]
    end

{{< /mermaid >}}

## Desired properties of Hash Functions.

Few properties which I think are very crucial for Hash Functions to have are as follows-

1. Uniformity
2. Efficiency
3. Applicability
4. Determinism

Some properties like the range of a Hash Function depends on its application. So, a Hash Function can have a well-defined range or a variable range. An example would be if we want our hash function to be used for some sort of indexing for a hash table then having a well-defined range is necessary because of the system constraints.

### Uniformity
Uniformity simply means that a Hash Function should have a uniform distribution over its range because if it doesn't have, then the chances of collision would go up and it will lead to collisions. If a Hash Function is not designed to achieve uniformity then it may be the case that
{{< katex >}}
\forall x_i \in \xi, \hat h (x_i) = C
{{< /katex >}} viz, all the keys get mapped to the same bucket
which we strictly don't want as it negates the purpose of having a Hash Function.

### Efficiency
As the name suggests the Hash Function should be efficient in terms of cost of calculation. An example is let's say we are using a custom hash map in C++, we wrote our hash function which takes 1 sec to calculate the hash value, Now, every insertion in the data structure will take 1 second which is pretty bad. The crux is
{{< hint warning>}}
It should not be the case where Linear Search becomes faster (inclusive insertion/deletions/updates) than the Hash Map because of the overhead introduced by the Hash Function.
{{< /hint >}}

### Applicability
Applicability means that our Hash Function should be capable enough to hash different types and different sizes of input. It should have a parameter for seed. This Hash Function would be more applicable than the one which doesn't have these features.


### Determinism
This simply means that it should be deterministic i.e.
For a given hash function
{{< katex >}}
\hat \sigma(\xi), \xi \in \{x_0,..,x_N\},
{{< /katex >}}
If we iterate through the set {{< katex >}} \xi {{< /katex >}} and calculate the hash for all the keys then,
{{< katex display >}}
\forall x_i, x_j \in \xi, x_i = x_j \implies \hat \sigma (x_i) = \hat \sigma (x_j)
{{< /katex >}}
viz, The same input should result in the same hash output agnostic of any iteration or condition.


## Test of a good Hash Function.

### Chi-Squared Test: {{< katex >}} \mu(\hat h) {{< /katex >}}
The uniformity of the distribution of a hash function can be evaluated using the Chi-Squared test.
Assuming we have

{{< katex >}} m-buckets, n-keys, b_j  {{< /katex >}} is the number of elements in bucket j, then
{{< hint info >}}
{{< katex display >}} \mu(\hat h) := \frac{\sum_{j=0}^{m-1} b_j(b_j+1)/2}{\frac{n}{2m}(n+2m-1)}  {{< /katex >}}
{{< /hint >}}

### Case Study

Let's say we have a hash function
{{< katex >}} \hat \sigma(x)  {{< /katex >}} such that
{{< katex display >}} \mu(\hat \sigma) := \frac{\sum_{j=0}^{m-1} b_j(b_j+1)/2}{\frac{n}{2m}(n+2m-1)}  {{< /katex >}}
Now to simplify thing here, let's say
{{< katex >}}  n = k.m {{< /katex >}} i.e. total number keys is a multiple of total number of buckets.
{{< katex display >}} \mu(\hat \sigma) := \frac{\sum_{j=0}^{m-1} b_j(b_j+1)/2}{\frac{k.m}{2m}(k.m+2m-1)}  {{< /katex >}}
{{< katex display >}} \mu(\hat \sigma) := \frac{2.\sum_{j=0}^{m-1} b_j(b_j+1)/2}{k.m(k+2-1/m)}  {{< /katex >}}
{{< katex display >}} \mu(\hat \sigma) := \frac{\sum_{j=0}^{m-1} b_j(b_j+1)}{k.m(k+2-1/m)}  {{< /katex >}} Assuming m to be large we can ignore the 1/m term. The equation becomes -
{{< katex display >}} \mu(\hat \sigma) := \frac{\sum_{j=0}^{m-1} b_j(b_j+1)}{m.k(k+2)}  {{< /katex >}}
Now we can see how the Mu changes as a function of distribution and the keys to bucket ratio of the Hash Function.
{{< hint info >}}
Note: The distribution signifies how the Hash Function distributes the set of keys to a set of buckets. The keys to bucket ratio indicates how the performance of a Hash Map changes as the number of keys/buckets changes.
{{< /hint >}}

Eg No.|{{< katex >}} k {{< /katex >}}  | {{< katex >}} \{b_0, b_1, ..., b_{m-1} \} {{< /katex >}}  |  {{< katex >}} \mu(\hat \sigma) := \frac{\sum_{j=0}^{m-1} b_j(b_j+1)}{m.k(k+2)} {{< /katex >}}
---|--------------------------------------------------------|-------- |-----
1  |0.01    | 1% of {{< katex >}} b_j {{< /katex >}} are 1   | {{< katex display >}} = \frac{2m/100}{m0.01(0.01+2)} = 0.995 {{< /katex >}}
2  | 0.01    | 0.1% of {{< katex >}} b_j {{< /katex >}} are 10    | {{< katex display >}} = \frac{110m/1000}{m0.01(0.01+2)} = 5.472 {{< /katex >}}
3  | 0.1    | 10% of {{< katex >}} b_j {{< /katex >}} are 1    | {{< katex display >}} = \frac{2m/10}{m0.1(0.1+2)} = 0.952 {{< /katex >}}
4 | 0.1    | 1% of {{< katex >}} b_j {{< /katex >}} are 10    | {{< katex display >}} = \frac{110m/100}{m0.1(0.1+2)} = 5.238 {{< /katex >}}

The value of Mu/chi-squared test is said to be in range (0.95 - 1.05) if a Hash Function has a uniform distribution. From above example number 1 and 3 we can see that if few % buckets has only one key in them, then the Mu has a value between the former range. And in other examples, few % buckets has 10 (more than 1) keys in them which caused Mu to be very high. It signifies that the distribution is not so good in those cases.

### Handling Collisions.
There are multiple approaches to handle collisions.
1. Chaining
2. Linear probing
3. k-level hashing
4. Tree chaining

The abstract idea is to store the two keys which has the same hash value. Either we can create a linked list for every bucket, either we can put the collision key into the next bucket in the hashmap as we do in linear probing, either we can maintain another level of hash map (with a different hash function) at every bucket in the main hash map or we can maintain a BST for every bucket.


## Hash Map in Python or Python Dictionaries.
This idea of Hash Map is now known as Python Dictionaries provided as an abstraction in python. As per my research, I found that the python dictionaries use inbuilt hash function named *hash(x)*. Th *hash* internally uses [**ScipHash**](https://github.com/python/cpython/blob/master/Python/pyhash.c). As per wikipedia [ScipHash](https://en.wikipedia.org/wiki/Cryptographic_hash_function) is used in Hash Maps of many languages like Perl 5, Python (starting in version 3.4), Raku, Ruby,  Rust, systemd, OpenDNS, Haskell, OpenBSD, Swift, Bitcoin (for short transaction IDs), Bloomberg BDE as a C++ object hasher. The Pyhton *hash* supports all the **immutable objects** as its input. Few examples of *hash* are -
{{< hint danger >}}
All the mutable objects like Lists, Dictionaries cannot be hashed. One way to hash a list is to cast it to a tuple.
{{< /hint >}}

```
$ python
Python 3.7.6 (default, Dec 30 2019, 19:38:26)
[Clang 11.0.0 (clang-1100.0.33.16)] on darwin
Type "help", "copyright", "credits" or "license" for more information.

>>> hash(1)
1

>>> hash(2)
2

>>> hash(-1)
-2

>>> hash(20)
20

>>> hash(999999999999999999)
999999999999999999

>>> hash(9999999999999999999)
776627963145224195

>>> hash(0.1)
230584300921369408

>>> hash(0.3)
691752902764108160

>>> hash('Hanchau is Awesome!!!')
8294309964540925058

>>> hash([1,2,3])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'

>>> hash(tuple([1,2,3]))
2528502973977326415

>>> #AN EXAMPLE OF COLLISION
>>> hash(-1)
-2
>>> hash(-2)
-2
>>> hash(-1) is hash(-2)
True

>>> hash(100) is -1 * hash(-100)
True

>>> hash({1,2,3})
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'set'

>>> # FROZEN SETS ARE IMMUTABLE HENCE HASHABLE
>>> hash(frozenset({1,2,3}))
-272375401224217160
```
Well at first I thought to cover Cryptographic Hash Functions in the same post but let's save it for another day.

Thanks & Cheers!!

## References

- [Hash Function](https://en.wikipedia.org/wiki/Hash_function)
- [Hash Tables](https://en.wikipedia.org/wiki/Hash_table)
- [Hashing](https://medium.com/tech-tales/what-is-hashing-6edba0ebfa67)
- [Snippet of a Hash Function](http://www.azillionmonkeys.com/qed/hash.html)
- [Make your own Hash Function](https://www.includehelp.com/data-structure-tutorial/hashing.aspx)
- [SipHash](https://en.wikipedia.org/wiki/SipHash)
- [Cryptographic Hash Functions](https://en.wikipedia.org/wiki/Cryptographic_hash_function)

## Cool Videos to watch.
---

{{< youtube z0lJ2k0sl1g >}}

<br>

---

{{< youtube Vdrab3sB7MU >}}

<br>
