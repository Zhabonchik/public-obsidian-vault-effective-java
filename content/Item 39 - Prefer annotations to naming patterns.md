Prefer custom annotations over naming patterns when designing APIs or frameworks. Naming patterns fail silently on typos, cannot enforce placement on appropriate program elements, and cannot pass parameter data cleanly. Annotations eliminate these issues by providing compile-time type checking, explicit target constraints, and flexible parameter support.

```java
@Retention(RetentionPolicy.RUNTIME)  
@Target(ElementType.METHOD)  
public @interface Test {  
  
}

@Retention(RetentionPolicy.RUNTIME)  
@Target(ElementType.METHOD)  
public @interface ExceptionTest {  
  
    Class<? extends Throwable> value();  
  
}

public class TestRunner {  
  
    public static void run(Class<?> clazz) {  
        int passedNumber = 0;  
        int failedNumber = 0;  
  
        // Create an instance to invoke non-static methods  
        Object testInstance;  
        try {  
            testInstance = clazz.getDeclaredConstructor().newInstance();  
        } catch (Exception e) {  
            testInstance = null; // Fallback to null if zero-arg constructor is missing  
        }  
  
        for (Method method : clazz.getDeclaredMethods()) {  
            if (method.isAnnotationPresent(ExceptionTest.class)) {  
                Class<? extends Throwable> expectedException = method.getAnnotation(ExceptionTest.class).value();  
                try {  
                    method.invoke(testInstance);  
                    failedNumber++; // Test failed because no exception was thrown  
                } catch (InvocationTargetException e) {  
                    if (expectedException.isInstance(e.getCause())) {  
                        passedNumber++;  
                    } else {  
                        failedNumber++;  
                    }  
                } catch (Exception e) {  
                    failedNumber++; // Reflection invocation error  
                }  
            } else if (method.isAnnotationPresent(Test.class)) {  
                try {  
                    method.invoke(testInstance);  
                    passedNumber++;  
                } catch (Exception e) {  
                    failedNumber++;  
                }  
            }  
        }  
  
        IO.print("Passed: %d, Failed: %d".formatted(passedNumber, failedNumber));  
    }  
}

public class SampleTests {  
  
    @Test  
    public static void test() {}  
  
    @Test  
    public static void testRuntimeException() {  
        throw new RuntimeException("test");  
    }  
  
    @ExceptionTest(value = IndexOutOfBoundsException.class)  
    public static void testIndexOutOfBoundsException() {  
        throw new IndexOutOfBoundsException("test");  
    }  
  
    @ExceptionTest(value = IndexOutOfBoundsException.class)  
    public static void testNotIndexOutOfBoundsException() {  
        throw new IllegalArgumentException("test");  
    }  
  
    public void testIgnoreMethod() {}  
  
}

```