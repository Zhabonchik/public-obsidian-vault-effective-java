**Core Principle:** Inheritance breaks encapsulation across package boundaries unless the class is explicitly designed and documented for extension.

**When to Use Inheritance:**
- Only when a genuine **"is-a"** relationship exists AND both classes are in the **same package** (or the superclass was explicitly designed and documented for extension).

**Why Composition is Better:**
- **Preserves Encapsulation:** Gives you a new class with private fields referencing instances of existing classes. You depend only on public interfaces, not fragile internal implementation details.
- **Eliminates Self-Use Bugs:** Prevents double-counting or side-effects caused by a superclass internally calling its own overridable methods.
- **Maximum Flexibility (Decorator Pattern):** A single forwarding class implementing an interface can wrap _any_ existing implementation of that interface and add behavior seamlessly (e.g., adding counting logic to _any_ `Set`).

**Trade-offs / Drawbacks of Wrapper Classes:**
- **The SELF Problem:** Wrapper classes cannot be easily used with callback frameworks because wrapped instances don't know about their outer wrappers.
- **Minor Boilerplate:** Requires writing forwarding methods (though IDEs generate these easily).

```java
import java.util.Collection;  
import java.util.Iterator;  
import java.util.Set;  
  
public class CountingHashSet<E> extends ForwardingHashSet<E> {  
  
    private int addCount = 0;  
  
    public CountingHashSet(Set<E> set) {  
        super(set);  
    }  
  
    @Override  
    public boolean add(E e) {  
        addCount++;  
        return super.add(e);  
    }  
  
    @Override  
    public boolean addAll(Collection<? extends E> c) {  
        addCount += c.size();  
        return super.addAll(c);  
    }  
  
    public int getAddCount() {  
        return addCount;  
    }  
}  
  
class ForwardingHashSet<E> implements Set<E> {  
  
    private final Set<E> set;  
  
    public ForwardingHashSet(Set<E> set) {  
        this.set = set;  
    }  
  
    @Override  
    public int size() {  
        return set.size();  
    }  
  
    @Override  
    public boolean isEmpty() {  
        return set.isEmpty();  
    }  
  
    @Override  
    public boolean contains(Object o) {  
        return set.contains(o);  
    }  
  
    @Override  
    public Iterator<E> iterator() {  
        return set.iterator();  
    }  
  
    @Override  
    public Object[] toArray() {  
        return set.toArray();  
    }  
  
    @Override  
    public <T> T[] toArray(T[] a) {  
        return set.toArray(a);  
    }  
  
    @Override  
    public boolean add(E e) {  
        return set.add(e);  
    }  
  
    @Override  
    public boolean remove(Object o) {  
        return set.remove(o);  
    }  
  
    @Override  
    public boolean containsAll(Collection<?> c) {  
        return set.containsAll(c);  
    }  
  
    @Override  
    public boolean addAll(Collection<? extends E> c) {  
        return set.addAll(c);  
    }  
  
    @Override  
    public boolean retainAll(Collection<?> c) {  
        return set.retainAll(c);  
    }  
  
    @Override  
    public boolean removeAll(Collection<?> c) {  
        return set.removeAll(c);  
    }  
  
    @Override  
    public void clear() {  
        set.clear();  
    }  
  
    @Override  
    public boolean equals(Object o) {  
        return set.equals(o);  
    }  
  
    @Override  
    public int hashCode() {  
        return set.hashCode();  
    }  
  
    @Override  
    public String toString() {  
        return set.toString();  
    }  
}
```