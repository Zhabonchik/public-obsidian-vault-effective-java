
**The 6 Core Functional Interfaces**
Most of the 43 standard functional interfaces in `java.util.function` derive from six basic types:
- `UnaryOperator<T>`: Takes one `T`, returns a `T` (`T apply(T t)`)
- `BinaryOperator<T>`: Takes two `T`s, returns a `T` (`T apply(T t1, T t2)`)
- `Predicate<T>`: Takes a `T`, returns a `boolean` (`boolean test(T t)`)
- `Function<T,R>`: Takes a `T`, returns an `R` (`R apply(T t)`)
- `Supplier<T>`: Takes no arguments, returns a `T` (`T get()`)
- `Consumer<T>`: Takes a `T`, returns nothing (`void accept(T t)`)

**Key Guidelines**
- **Avoid Boxed Primitives:** Do not use basic functional interfaces with boxed primitive types (e.g., `Predicate<Integer>` or `Function<Double, Long>`). Always use primitive specializations like `IntPredicate`, `DoubleConsumer`, or `LongToDoubleFunction` to avoid auto-boxing performance penalties.
- **When to Write Custom Interfaces:** Write a custom interface (like `Comparator<T>` instead of `BiFunction<T,T,Integer>`) only if it requires a distinct, highly descriptive name, enforces a strict custom contract, or benefits from custom default methods.
- **Always Use `@FunctionalInterface`:** Always annotate custom functional interfaces with `@FunctionalInterface`. This documents intent, enforces single-abstract-method constraints at compile time, and prevents maintainers from accidentally adding abstract methods later.
- **Beware Overloading Ambiguity:** Do not overload methods that accept different functional interfaces in the same argument position (e.g., overloading a method with both `Callable<V>` and `Runnable`). It creates type inference ambiguity for clients passing lambdas.