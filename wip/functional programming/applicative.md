---
creation date: 2022-11-23 15:08
modification date: Wednesday, 23rd November 2022, 23:13:12
tags: engineering/functional-programming
---

# Applicative

## Definition

Applicative is a sub-type of [[functor]] with additional available functions: `pure` and `ap`.

```javascript
function pure<A>(A) : Foo<A>  
function ap<A, B>(Foo<A => B>, Foo<A>) : Foo<B>
```

`pure` should take a value of any type and return an applicative functor with that value inside it. When we say inside it, we're using the box analogy again, even though we've seen that it doesn't always stand up to scrutiny. But the a -> f a type declaration is still pretty descriptive. We take a value, and we wrap it in an applicative functor that has that value as the result inside it.  A better way of thinking about pure would be to say that it takes a value and puts it in some default (or pure) context—a minimal context that still yields that value.

The `<*>` function is really interesting. It has a type declaration of `f (a -> b) -> f a -> f b`. Does this remind you of anything? Of course, `fmap : : (a -> b) -> f a -> f b`. It's a sort of a beefed-up fmap. Whereas fmap takes a function and a functor and applies the function inside the functor, `<*>` takes a functor that has a function in it and another functor and sort of extracts that function from the first functor and then maps it over the second one. When I say extract, I actually sort of mean run and then extract, maybe even sequence. We'll see why soon.

`pure` places a value into a minimal context, and `ap` serves the purpose of function application within a context. `map` lets you apply a normal function to a value inside a functor, getting a functor that holds a new value in an unchanged functor context. `ap` goes further; given a function and a value that are both already inside functor contexts, it combines these contexts and puts the result of the function application into the new context.

So another way to look at `ap` is that it lets us turn a function _within a context into a function that operates _on contexts_. Effectively `ap` can let us lift a function through a functor.

The most important takeaway while learning to use applicatives is that `ap` behaves like normal function application, just inside of a functor, and that `pure` produces contexts that can be combined with other contexts without modifying the other context.


---
Applicatives take it to the next level. With an applicative, our values are wrapped in a context, just like Functors:

![](https://camo.githubusercontent.com/792ecd2f6bb3dbaf41dccdc23d6ebe5a0d1543e7e2ffec531a772fb0dccf9799/687474703a2f2f616469742e696f2f696d67732f66756e63746f72732f76616c75655f616e645f636f6e746578742e706e67)

But our functions are wrapped in a context too!

![](https://camo.githubusercontent.com/bfd909e988866e441c92a1a8f8cebb3d4f1fe06519b0ede6c0d49080c52dbc5a/687474703a2f2f616469742e696f2f696d67732f66756e63746f72732f66756e6374696f6e5f616e645f636f6e746578742e706e67)

Yeah. Let that sink in. Applicatives don’t kid around. Applicative defines `*` (`<*>` in Haskell), which knows how to apply a function wrapped in a context to a value wrapped in a context:

![](https://camo.githubusercontent.com/7a69c8d02554f4fb5b5a8670f1aae57c114284fdcb5d8b8800a0eed380cf78f4/687474703a2f2f616469742e696f2f696d67732f66756e63746f72732f6170706c696361746976655f6a7573742e706e67)

i.e.:

```python
>>> Just(lambda x: x+3) * Just(2) == Just(5)
True
```

Using `*` can lead to some interesting situations. For example:

```python
>>> List([lambda x: x*2, lambda y: y+3]) * List([1, 2, 3])
[2, 4, 6, 4, 5, 6]
```

![](https://camo.githubusercontent.com/367abfb69c81b3fc6c06b55a1028a0719a2c8b7047cfdf3cfb78b127317a926e/687474703a2f2f616469742e696f2f696d67732f66756e63746f72732f6170706c696361746976655f6c6973742e706e67)

**Here’s something you can do with Applicatives that you can’t do with Functors.** How do you apply a function that takes two arguments to two wrapped values?

```python
>>> (lambda x,y: x+y) % Just(5)
Just functools.partial(<function <lambda> at 0x1003c1bf8>, 5)

>>> Just(lambda x: x+5) % Just(5)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for <<: 'Just' and 'Just'

```


Applicatives:

```python
>>> (lambda x,y: x+y) % Just(5)
Just functools.partial(<function <lambda> at 0x1003c1bf8>, 5)

>>> Just(lambda x: x+5) * Just(5)
Just 10
```

`Applicative` pushes `Functor` aside. “Big boys can use functions with any number of arguments,” it says. “Armed with `%`and `*`, I can take any function that expects any number of unwrapped values. Then I pass it all wrapped values, and I get a wrapped value out! AHAHAHAHAH!”

```python
>>> (lambda x,y: x*y) % Just(5) * Just(3)
Just 15
```

And hey! There’s a method called `lift_a2` that does the same thing:

```python
>>> Just(5).lift_a2(lambda x,y: x*y, Just(3))
Just 15
```
