If a class is not supposed to be instantiated (utility class containing only static methods), then the best way to prevent user from creating an instance of the class is to make its **constructor private**. Also the class should be made **final** - we don't want to extend it.

```java
public final class StringUtils {  
  
    private StringUtils() {  
        throw new AssertionError("Utility class — do not instantiate.");  
    }  
  
    public static boolean isNullOrEmpty(String str) {  
        return str == null || str.isEmpty();  
    }  
  
    public static String reverse(String str) {  
        if (str == null) {  
            return null;  
        }  
  
        return new StringBuilder(str).reverse().toString();  
    }  
}
```