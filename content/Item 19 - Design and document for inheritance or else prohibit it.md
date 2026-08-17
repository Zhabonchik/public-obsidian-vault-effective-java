As mentioned in the Item 18 extending classes can result into unexpected behavior. The biggest problem is when one overridable method uses another overridable method.

Designing for inheritance:
- If you understand that your class will likely be extended, then you should explicitly document the logic of overridable methods so that clients understood the pitfalls, which violates the rule of self-descriptive code and encapsulation though.
- Move the reusable logic from another overridable method into a private method and use the private method in both overridable methods instead.
- Expose well-chosen protected methods/fields to give subclasses sufficient access to internal mechanics.
- Never use overridable methods in constructors.

Remember, that once your class is presented to others (released) you will likely be not able to modify it if it is designed for extension. Otherwise make it final / use static factory methods to avoid inheritance.