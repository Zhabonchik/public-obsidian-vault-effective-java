Use enums over primitive `int` or `String` constants whenever you need a fixed set of constants known at compile time.

**Core Advantages Over Int Constants**
- **Type Safety & Namespaces:** Enums enforce strict compile-time types so different enum types cannot be mixed up. They provide their own namespace, eliminating the need for artificial naming prefixes (e.g., `ELEMENT_FIRE`).
- **Binary Compatibility:** Adding, reordering, or renaming enum constants does not break binary compatibility. While changing `int` constants silently bakes stale primitive values into compiled client `.class` files, removing an enum constant surfaces clean compile-time or runtime errors (`NoSuchFieldError`) instead of silent bugs.
- **Built-in Language Support:** Out of the box, enums provide readable names (`toString()`), string parsing (`valueOf()`), array iteration (`values()`), natural ordering (`Comparable`), and serialization (`Serializable`).

**Advanced Features & Best Practices**
- **Constant-Specific Data & Behavior:** As full-fledged classes, enums can host fields, constructors, and methods. You can declare an abstract method in the enum and override it per constant to bind unique logic directly to values (e.g., specific arithmetic operations for `PLUS` vs `MINUS`).
- **Strategy Enum Pattern:** When multiple constants share identical non-default behavior (such as overtime pay logic for weekend vs. weekday shifts), delegate that logic to a nested strategy enum passed via the constructor. This avoids duplicate code and fragile `switch` statements when adding new constants later.
- **Immutability & Extension:** Enums are implicitly `final` and cannot be subclassed or extended via class inheritance. Keep all fields `final` to guarantee immutability and thread safety. Use them whenever you have a set of constants known at compile time, even if the set will expand in future releases.

```java
  
public enum PayrollDay {  
  
    MONDAY(PayType.WEEKDAY),  
    TUESDAY(PayType.WEEKDAY),  
    WEDNESDAY(PayType.WEEKDAY),  
    THURSDAY(PayType.WEEKDAY),  
    FRIDAY(PayType.WEEKDAY),  
    SATURDAY(PayType.WEEKEND),  
    SUNDAY(PayType.WEEKEND);  
  
    private final PayType payType;  
  
    PayrollDay(PayType payType) {  
        this.payType = payType;  
    }  
  
    public double pay(double hoursWorked, double baseRate) {  
        return payType.calculatePayment(hoursWorked, baseRate);  
    }  
  
  
    private enum PayType {  
  
        WEEKDAY {  
            public double calculatePayment(double hoursWorked, double baseRate) {  
                double overtimeHours = Math.max(0, hoursWorked - WORKING_HOURS);  
                double baseHours = hoursWorked - overtimeHours;  
  
                return (baseHours + overtimeHours * WEEKDAY_OVERTIME_COEFFICIENT) * baseRate;  
            }  
        },  
        WEEKEND {  
            @Override  
            public double calculatePayment(double hoursWorked, double baseRate) {  
                return hoursWorked * baseRate * WEEKEND_COEFFICIENT;  
            }  
        };  
  
        private static final int WORKING_HOURS = 8;  
        private static final double WEEKEND_COEFFICIENT = 2;  
        private static final double WEEKDAY_OVERTIME_COEFFICIENT = 1.5;  
  
        public abstract double calculatePayment(double hoursWorked, double baseRate);  
    }  
  
}
```