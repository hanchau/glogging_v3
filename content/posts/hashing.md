+++
author = "hanchau"
title = "Hashing"
date = "2020-05-10"
description = "Hashing, A popular choice across all fields of CS"
tags = [
    "Hashing",
    "Hash Functions",
    "Hash Table",
    "Python Dictionaries",
    "Cryptography"
]
categories = [
    "Concept",
]
+++

## A Brief History.

Arousal of an idea parallelly at multiple places is indicative of its need in the ecosystem. Like many ideas in Computer Science, Hashing was also introduced independently by different scientists. According to [Wikipedia](https://en.wikipedia.org/wiki/Hash_table#History), In 1953, At IBM, one computer scientist named Hans Pete Luhn wrote an internal memorandum that used Hashing (with Chaining), and about the same time, a group of scientists Gene Amdahl, Elaine M. McGraw, Nathaniel Rochester, and Arthur Samuel wrote a program using Hashing. After that, there has been a lot of work/research around Hashing. I can't think of a computer science field where we don't use Hashing. So Let's move right on to the concept.

## Concepts/Definitions.

### Hash Function
The Definitions of an Hash Function is pretty straight forward -
A Hash Function is a function {{< katex >}}\hat h{{< /katex >}} which maps a set of arbitrary number of elements to a set of fixed number of elements i.e.
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
{{< katex >}}\hat h{{< /katex >}} we get the same output i.e.
{{< hint info >}}
{{< katex display >}} x_1, x_2 \in \xi,  x_1 \neq x_2, but, \hat h(x_1) = \hat h(x_2) {{< /katex >}}
{{< /hint >}}

### Hash Table/ Hash Map
As the name suggests, A Hash Table is a table made up of 2 primary fields, key and value. The key field stores the keys from the set
{{< katex >}}\xi{{< /katex >}}
and the value fied stores the address of the key's corresponding value in the memory.



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
    lion --> 4 --> A
    bat --> 7 --> B
    subgraph keys
    dog --> cat --> lion --> bat --> me
    end
    subgraph hash
    0 --> 1 --> 4 -->7 -->8
    end
    subgraph memory
    A["0X123, hiss"] --> B["0X234, roar"] --> C["0X324, bark"]
    end

{{< /mermaid >}}


## Test of a good Hash Function.

### Chi Squared Test: {{< katex >}} \mu(\hat h) {{< /katex >}}
The uniformity of the distribution of a hash function can be evaluated using the chi-squared test.
Assuming we have

{{< katex >}} m-buckets, n-keys, b_j  {{< /katex >}} is the number of elements in bucket j, then
{{< hint info >}}
{{< katex display >}} \mu(\hat h) := \frac{\sum_{j=0}^{m-1} b_j(b_j+1)/2}{\frac{n}{2m}(n+2m-1)}  {{< /katex >}}
{{< /hint >}}

### An Example
Let's say we have a hash function

{{< katex >}} \hat \sigma(x)  {{< /katex >}} such that
{{< katex  >}} \nexists x_1, x_2 \in \xi{{< /katex >}} for which
{{< katex >}} \hat \sigma(x_1) = \hat \sigma(x_2) {{< /katex >}}
{{< katex >}} \implies  \forall j , b_j = 1  {{< /katex >}} therefore
{{< katex display >}} \mu(\hat \sigma) := \frac{m}{\frac{n}{2m}(n+2m-1)}{{< /katex >}} Now if m >> n
{{< katex display >}} \mu(\hat \sigma) := \frac{m}{\frac{n}{2m}(n+2m-1)}{{< /katex >}}

## Expectation vs Reality of Hash Function's Properties.


### Handling Collisions.


## Popular Hash Functions.


## Hash Map in python  Dictionaries.


## Use Cases.


## Cryptographic Hash Functions.


## References

- [Hash Function](https://en.wikipedia.org/wiki/Hash_function)
- [Hash Tables](https://en.wikipedia.org/wiki/Hash_table)
- [Hashing](https://medium.com/tech-tales/what-is-hashing-6edba0ebfa67)


## Cool Videos to watch.
---

{{< youtube z0lJ2k0sl1g >}}

<br>

---

{{< youtube Vdrab3sB7MU >}}

<br>
