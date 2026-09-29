### 1. Fundamental Differences

- **Identity vs. Value:** Primitives have only their values. Boxed primitives have object identities distinct from their values (two boxed primitive instances can hold the same value but have different reference identities).
    
      
    
- **Nullability:** Primitives always hold functional values (defaulting to zero/false). Boxed primitives can be `null`.
    
      
    
- **Efficiency:** Primitives are significantly more time- and space-efficient than boxed primitives.
    
      
    

### 2. Common Pitfalls & Bugs

- **Identity Comparison (`==`):** Applying the `==` operator to boxed primitives compares their memory references, not their numeric values. This leads to subtle bugs (e.g., `Integer` instances evaluated as unequal even with identical numeric values).
    
      
    
- **Unboxing `null` (`NullPointerException`):** In almost every operation mixing primitives and boxed primitives, the boxed primitive is automatically unboxed. If the boxed value is `null`, it throws a `NullPointerException`.
    
      
    
- **Performance Degradation:** Unintentional autoboxing inside tight loops or repeated operations creates thousands of unnecessary objects, causing severe CPU and memory overhead (e.g., using `Long` instead of `long` as a loop counter/accumulator).
    
      
    

### 3. Valid Use Cases for Boxed Primitives

- **Collections & Generics:** Java collections (like `List`, `Set`, `Map`) and generic type parameters require object references because Java does not support primitives in generics (e.g., `List<Integer>` instead of `List<int>`).
    
      
    
- **Type Parameters:** Parameterized classes or methods (e.g., `ThreadLocal<Integer>`).
    
      
    
- **Reflection:** Reflective method invocations demand object types.
    
      
    

Which item from _Effective Java_ would you like to tackle next?