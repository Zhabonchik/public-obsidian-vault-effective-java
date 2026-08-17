Reasons to prefer interfaces to abstract classes:
- A class can implement multiple interfaces but extend only one class
- Interfaces help to utilize the 'Interface Segregation' principle
- Interfaces can be used to declare a contract for an additional behavior (Mixin), not the main one (Serializable, Autocloseable)
- Interfaces are better for the backward compatibility. You can always implements an interface within an existing class while it will be problematic with the extension of a class (breaking the hierarchy)
- Interfaces allow flexible combinations, when classes result into combinatorial explosion (2^n classes in case of n variants of behavior)

Rules of creating interfaces:
- Interfaces can have only public static final fields and the following methods: public, public static, default, private, private static
- default methods can't provide implementation for equals(), hashCode(), toString() 
- Provide a default implementation for an interface method if possible
- Create Skeleton (AbstractInterface) implementation in a form of an Abstract class with implementations for the interface's complex methods. This allows classes that already have a superclass to delegate interface methods to an internal instance of the skeletal implementation
- Provide documentation as per Item 19

```java
public interface IntSequence {  
    // --- Primitive Methods (Must be implemented by concrete storage classes) ---  
    int size();  
    int get(int index);  
  
    // --- Derived / Utility Methods ---  
    boolean isEmpty();  
    boolean contains(int value);  
    int[] toArray();  
  
    // --- Object Methods (Cannot be default methods in an interface!) ---  
    @Override  
    String toString();  
  
    @Override  
    boolean equals(Object o);  
  
    @Override  
    int hashCode();  
}

public abstract class AbstractIntSequence implements IntSequence {  
  
    @Override  
    public boolean isEmpty() {  
        return size() == 0;  
    }  
  
    @Override  
    public boolean contains(int value) {  
        for (int i = 0; i < size(); i++) {  
            if (get(i) == value) {  
                return true;  
            }  
        }  
  
        return false;  
    }  
  
    @Override  
    public int[] toArray() {  
        int[] array = new int[size()];  
        for (int i = 0; i < size(); i++) {  
            array[i] = get(i);  
        }  
        return array;  
    }  
  
    @Override  
    public String toString() {  
        if (isEmpty()) {  
            return "[]";  
        }  
  
        StringBuilder stringBuilder = new StringBuilder();  
        stringBuilder.append("[");  
        for (int i = 0; i < size() - 1; i++) {  
            stringBuilder.append(get(i));  
            stringBuilder.append(", ");  
        }  
          
        return stringBuilder.append(get(size() - 1)).append("]").toString();  
    }  
  
    @Override  
    public boolean equals(Object o) {  
        if (this == o) return true;  
        if (!(o instanceof IntSequence other)) return false;  
        if (size() != other.size()) return false; // Early exit on size mismatch  
  
        for (int i = 0; i < size(); i++) {  
            if (get(i) != other.get(i)) return false;  
        }  
  
        return true;  
    }  
  
    @Override  
    public int hashCode() {  
        int result = 1;  
        for (int i = 0; i < size(); i++) {  
            result = 31 * result + Integer.hashCode(get(i));  
        }  
        return result;  
    }  
}

public class ArrayIntSequence extends AbstractIntSequence {  
  
    private final int[] array;  
  
    private ArrayIntSequence(int[] array) {  
        this.array = Arrays.copyOf(array, array.length);  
    }  
  
    public static ArrayIntSequence of(int[] array) {  
        return new ArrayIntSequence(array);  
    }  
  
    @Override  
    public int size() {  
        return array.length;  
    }  
  
    @Override  
    public int get(int index) {  
        return array[index];  
    }  
}

```