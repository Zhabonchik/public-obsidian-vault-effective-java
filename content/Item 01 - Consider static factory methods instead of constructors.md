Before writing constructors consider writing static factory methods (don't confuse with design patterns).

The benefits of static factory methods in comparison to constructors are:
1) They can have descriptive names
2) They do not necessarily return a new instance
3) They can return any subclass of the return type class
4) Their return classes can vary as their parameters do
5) The class of the returned object may not exist when the static method is written

Limitations:
1) Classes without public or protected constructors can not be subclassed
2) Static factory methods are hard to find in documentation

Typical static method names:
- **from** — a type-conversion method
- **of** — aggregation method
- **valueOf** — alternative to from and of
- **instance** or **getInstance** — returns an instance described by its parameters
- **create** or **newInstance** — like above but each call returns a new instance
- **getType**, **newType**, **type** — are used when factory method resides in a different class than the returned object type (Files.newBufferedReader)