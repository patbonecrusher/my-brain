---
creation date: 2022-11-24 23:02
modification date: Thursday, 24th November 2022, 23:02:57
tags: engineering/functional-programming
---

# Glossary

## First-class function
If you can treat a function as a value, it is a first-class Function.
* You can assign it to a variable.
* You can pass it in as an argument to another function.
* You can return it from a function.

## High-order function
Functions that operate on other functions, either by taking them as arguments or by returning them.

## Pure function
A Pure Function is **a function (a block of code) that always returns the same result if the same arguments are passed**. It does not depend on any state or data change during a program's execution. Rather, it only depends on its input arguments.

## Do
**The do notation is just syntactic sugar for monadic composition**. On the surface, it looks a lot like imperative code, but it translates directly to a sequence of binds and lambda expressions.

Example for the IO Functor
*The result of mapping something over an I/O action will be an I/O action, so right off the bat, we use **do** syntax to glue two actions and make a new one.*

