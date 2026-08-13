When you **don't need** to override equals():
- when the standard implementation of Object class is suitable (no need to test for "logical equality")
- parent class implementation is suitable for its subclasses
- when a class is package-private or private and you know that its equals() method won't be called
- when each instance of the class is inherently unique (represent active entities rather than values)

You override the equals() method for classes that represent values. In order to satisfy the equals() contract the method should be:
- Reflexive. x.equals(x)
- Symmetric. If x.equals(y) then y.equals(x)
- Transitive. If x.equals(y) and y.equals(z) then x.equals(z)
- Consistent. If x.equals(y) returns true then it should always return true unless some values or equals() method is not changed/modified
- for any non-null reference a.equals(null) must be false

**The Inheritance Trap:** There is no way to extend an instantiable class and add a new value field while preserving the `equals()` contract (symmetry and transitivity). Composition should be used instead of inheritance in these cases.
Always use @Override annotation with the equals() method to check that you override, not overload the method.

Typical scenario for equals implementation:

```java
import java.util.Currency;  
  
public class Money {  
  
    private final long amountInCents;  
    private final Currency currency;  
  
    public Money(long amountInCents, Currency currency) {  
        this.amountInCents = amountInCents;  
        this.currency = Objects.requireNonNull(currency);  
    }  
  
    @Override  
    public boolean equals(Object o) {  
        if (this == o) {  
            return true;  
        }  
  
        if (!(o instanceof Money money)) {  
            return false;  
        }  
  
        return this.amountInCents == money.amountInCents
		    && this.currency.equals(money.currency);  
    }  
}
```