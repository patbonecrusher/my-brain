1.  A functor is a data type that implements the `Functor` abstract base class.
2.  An applicative is a data type that implements the `Applicative` abstract base class.
3.  A monad is a data type that implements the `Monad` abstract base class.
4.  A `Maybe` implements all three, so it is a functor, an applicative, and a monad.

What is the difference between the three?

![](https://camo.githubusercontent.com/81e694a403ef7f34e87435dcebe418188a3829a385698d84592e6309743520db/687474703a2f2f616469742e696f2f696d67732f66756e63746f72732f72656361702e706e67)

-   **functors**: you apply a function to a wrapped value using `map` or `%`
-   **applicatives**: you apply a wrapped function to a wrapped value using `*` or `lift`
-   **monads**: you apply a function that returns a wrapped value, to a wrapped value using ´|´ or `bind`