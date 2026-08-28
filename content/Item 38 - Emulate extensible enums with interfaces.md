While enums cannot be extended, you can emulate extensible enums by creating an interface and implementing it across multiple enum types. APIs accept the interface (or bounded enum class tokens), allowing clients to supply custom enum types alongside standard ones. Note that implementation code cannot be inherited between enum types.

```java
public interface Operation {  
  
    double apply(double x, double y);  
  
}

public enum BasicOperation implements Operation {  
  
    PLUS("+") {  
        public double apply(double x, double y) {  
            return x + y;  
        }  
    },  
    MINUS("-") {  
        public double apply(double x, double y) {  
            return x - y;  
        }  
    },  
    TIMES("*") {  
        public double apply(double x, double y) {  
            return x * y;  
        }  
    },  
    DIVIDE("/") {  
        public double apply(double x, double y) {  
            return x / y;  
        }  
    };  
  
    private final String symbol;  
  
    BasicOperation(String symbol) {  
        this.symbol = symbol;  
    }  
  
    public String getSymbol() {  
        return symbol;  
    }  
  
    @Override  
    public String toString() {  
        return getSymbol();  
    }  
}

public enum ExtendedOperation implements Operation {  
  
    EXPONENTIAL("^") {  
        public double apply(double x, double y) {  
            return Math.pow(x, y);  
        }  
    },  
    REMAINDER("%") {  
        public double apply(double x, double y) {  
            return x % y;  
        }  
    };  
  
    private final String symbol;  
  
    ExtendedOperation(String symbol) {  
        this.symbol = symbol;  
    }  
  
    public String getSymbol() {  
        return symbol;  
    }  
  
    @Override  
    public String toString() {  
        return getSymbol();  
    }  
}

public class Tester {  
  
    public static <T extends Enum<T> & Operation> void test(Class<T> opEnumType, double x, double y) {  
        for (Operation op : opEnumType.getEnumConstants()) {  
            System.out.printf("%f %s %f = %f%n", x, op, y, op.apply(x, y));  
        }  
    }  
  
    public static void test(Collection<? extends Operation> opSet, double x, double y) {  
        for (Operation op : opSet) {  
            System.out.printf("%f %s %f = %f%n", x, op, y, op.apply(x, y));  
        }  
    }  
  
}
```