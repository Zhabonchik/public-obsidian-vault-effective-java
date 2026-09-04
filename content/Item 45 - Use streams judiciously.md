Streams consist of an initial stream, 0 or more intermediate operations and 1 terminal operation. 
Streams work lazily which means computations start only after the terminal operation is reached.

**Stateless vs. Stateful Barriers**:
- **Stateless Operations** (`filter`, `map`, `flatMap`): Elements pass vertically one by one.
- **Stateful Operations** (`sorted`, `distinct`): These create a "pipeline barrier." A `sorted()` operation _must_ consume all upstream elements and buffer them in memory before it can determine the first element to pass downstream.

**Overusing streams makes program hard to read and maintain.**

In the absence of explicit types variable naming is very important in streams. Using helper methods is even more important.

When to use blocks of code:
- From a block of code you can read and modify local variables, from lambdas you can read only final and effectively-final variables.
- From a code block you can return from the enclosing method, break or continue an enclosing loop, or throw any declared checked exception. It is impossible to do so from lambda.

When to use lambdas:
- Transform or filter sequence of elements
- Combine sequence of elements in a single operation
- Accumulate sequence of elements, grouping them
- Search or filter a sequence of elements

If you are not sure what to use, streams or iterations, then try both approaches and choose the best one.