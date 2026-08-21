Standard generic containers (like `Set<E>` or `Map<K,V>`) fix the number of element types per container. To store arbitrary types in a single container, we use a **Typesafe Heterogeneous Container** by parameterizing the key using `Class<T>` (called a _type token_).
```java
public class Favorites {
    private Map<Class<?>, Object> favorites = new HashMap<>();

    public <T> void putFavorite(Class<T> type, T instance) {
        favorites.put(Objects.requireNonNull(type), type.cast(instance)); // Runtime check prevents raw type pollution
    }

    public <T> T getFavorite(Class<T> type) {
        return type.cast(favorites.get(type)); // Typesafe dynamic cast
    }
}
```
**Limitations:**
1. Cannot use non-reifiable types as keys (e.g., `List<String>.class` does not exist).
2. Malicious/raw `Class` usage requires `type.cast()` during insertion to maintain runtime safety.
   
Final task:
```java
public class LegacyCache {  
    // Feature 1: Typesafe Heterogeneous Container  
    private final Map<Class<?>, Object> map = new HashMap<>();  
  
    public <T> void put(Class<T> type, T instance) {  
        map.put(type, type.cast(instance));  
    }  
  
    public <T> T get(Class<T> type) {  
        return type.cast(map.get(type));  
    }  
  
    // Feature 2: Bulk processing  
    public <T> void addAll(Class<T> type, List<? extends T> items) {  
        for (var item : items) {  
            put(type, item);  
        }  
    }  
  
    // Feature 3: Varargs array creation  
    @SafeVarargs  
    public static <T> List<T> combine(T first, T... rest) {  
        List<T> result = new ArrayList<>(rest.length + 1);  
        result.add(first);  
        result.addAll(Arrays.asList(rest));  
        return result;  
    }  
}
```