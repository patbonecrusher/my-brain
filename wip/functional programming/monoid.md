---
creation date: 2022-11-23 15:08
modification date: Wednesday, 23rd November 2022, 15:08:06
tags: engineering/functional-programming
---

What is the similarity between number addition, string concatenation, array concatenation, and function composition?

A [monoid](https://en.wikipedia.org/wiki/Monoid "Monoid") is an algebraic structure intermediate between semigroups and groups and is a semigroup having an [identity element](https://en.wikipedia.org/wiki/Identity_element "Identity element"), thus obeying all but one of the axioms of a group: the existence of inverses is not required of a monoid.

The term Monoid comes from category theory. It describes a set of elements that has 3 special properties when combined with a particular operation, often named `concat`:

- The operation must combine two values of the set into a third value of the same set. If `a` and `b` are part of the set, then `concat(a, b)` must also be part of the set. In category theory, this is called a _magma_.
- The operation must be _associative_: `concat(x, concat(y, z))` must be the same as `concat(concat(x, y), z)`, where `x`, `y`, and `z` are any values in the set. No matter how you group the operation, the result should be the same as long as the order is respected.
- The set must possess a _neutral element_ in regard to the operation. If that neutral element is combined with any other value, it should not change it. `concat(element, neutral) == concat(neutral, element) == element`

Example monoid:
* Number addition
* String concatenation
* Function composition

---
## references
https://marmelab.com/blog/2018/04/18/functional-programming-2-monoid.html
