There can be 4 types of nested classes:
- static member class
- non-static member class
- anonymous class
- local class

If you need to use a class inside more than 1 method - make it a member class. If the member class needs to reference it's outer class - make it non-static, otherwise - static.
If a class will be used only inside a method and will be instantiated once - use anonymous class, otherwise - local class.

Why should we prefer static member classes to non-static? Because non-static classes hold a reference to the outer class which results into worse performance, memory-consumption and potential bugs. If the inner instance outlives the outer instance, it prevents garbage collection of the outer object—leading to **memory leaks**.
Static member classes can be created without a prior creation of an outer class and thus don't hold reference to it.

```java
public class CacheManager {  
  
    private final String cacheName;  
    private final List<CacheEntry> entries = new ArrayList<>();  
    private int hitCount = 0;  
  
    private CacheManager(String cacheName) {  
        this.cacheName = cacheName;  
    }  
  
    public static CacheManager newInstance(String cacheName) {  
        return new CacheManager(cacheName);  
    }  
  
    // --- NESTED CLASS 1 ---  
    // Helper class used to store key-value pairs inside the cache    private static class CacheEntry {  
  
        private final String key;  
        private final Object value;  
  
        private CacheEntry(String key, Object value) {  
            this.key = key;  
            this.value = value;  
        }  
  
        public String getKey() {  
            return key;  
        }  
  
        public Object getValue() {  
            return value;  
        }  
    }  
  
    // --- NESTED CLASS 2 ---  
    // Class representing a snapshot of current stats, returned to external callers    public record CacheStats(int totalItems, int hits) {  
  
        public void print() {  
            System.out.println("Stats -> Items: " + totalItems + ", Hits: " + hits);  
        }  
    }  
  
    public void put(String key, Object value) {  
        entries.add(new CacheEntry(key, value));  
    }  
  
    public CacheStats getStats() {  
        return new CacheStats(entries.size(), hitCount);  
    }  
}
```