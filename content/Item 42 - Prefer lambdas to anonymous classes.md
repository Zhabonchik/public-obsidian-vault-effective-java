Lambdas were introduced in Java 8 and have substituted anonymous classes in many use cases. Lambdas are used to implement functional interfaces - interfaces with exactly 1 abstract method.

Lambdas vs anonymous classes:
- lambdas are better for small (up to 3 lines) of code
- *this* in lambda refers to the enclosing class, while in anonymous class it refers to the anonymous class itself
- lambdas implement only functional interfaces, in other cases use anonymous class
- lambdas lack names and documentation
- lambdas should not be serialized

So, in general, don't use anonymous classes for function objects unless you need to create instances that aren't functional interfaces.
