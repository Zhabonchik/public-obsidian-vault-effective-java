### 1. The Core Rule & Benefits

- **Use Interfaces for Types:** If appropriate interface types exist, parameters, return values, fields, and local variables should all be declared using interface types (e.g., `Set<User> users = new HashSet<>();`).
    
- **Flexibility & Maintainability:** Decoupling your code from specific implementation classes allows you to swap out the underlying concrete class simply by changing the constructor call.
    

### 2. Switching Implementation Caveats

- **Behavioral Contracts:** The replacement implementation must satisfy the requirements of the surrounding code. For example, replacing a `HashSet` with a `TreeSet` changes iteration order (unsorted vs. sorted) and lookup complexity ($O(1)$ vs. $O(\log n)$).
    
- **Implementation-Specific Features:** If existing code relies on non-interface behavior (e.g., synchronization features or custom capacity tuning), changing the underlying class can introduce bugs or subtle regressions.
    

### 3. Exceptions to the Rule

- **Value Classes:** Standard value types (e.g., `String`, `Integer`, `BigInteger`) rarely have interfaces, so referring to the concrete class is required.
    
- **Class-Based Frameworks:** Frameworks or base classes where functionality is extended via inheritance rather than interface implementation (e.g., `java.io.OutputStream` or `java.util.TimerTask`).
    
- **Classes with Unique Capabilities:** Concrete classes that offer methods outside their standard interfaces (e.g., `PriorityQueue` or `LinkedHashMap`) when callers explicitly depend on those extra capabilities.