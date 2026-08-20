Instead of making your implementation suitable for a particular class make it Generic. This will allow you to create one class suitable for work with any object type. Also this will move the obligation of casting (Object to their class) from clients to compiler.

```java
public class FixedStack <E> {  
    private final E[] elements;  
    private int size = 0;  
  
    // Elements array will only contain E instances from push(E).
    // This is sufficient to ensure type safety, but the runtime
    // type of the array won't be E[]; it will always be Object[]!
    @SuppressWarnings("unchecked")  
    public FixedStack(int capacity) {  
        elements = (E[]) new Object[capacity];  
    }  
  
    public void push(E element) {  
        if (size == elements.length) {  
            throw new IllegalStateException("Stack is full");  
        }  
        elements[size++] = element;  
    }  
  
    public E pop() {  
        if (size == 0) {  
            throw new IllegalStateException("Stack is empty");  
        }  
        E result = elements[--size];  
        elements[size] = null; // Eliminate obsolete reference  
        return result;  
    }  
  
    public boolean isEmpty() {  
        return size == 0;  
    }  
}
```