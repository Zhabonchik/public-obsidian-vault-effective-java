- **Core Purpose:** `Optional<T>` explicitly signals in the return type that a value might be missing. It forces callers to handle the empty case without forcing you to throw checked exceptions or relying on callers to remember `null` checks.
    
- **Container Types & Primitives:**
    
    - **Containers:** Never return `Optional<List<T>>` or `Optional<Map<K,V>>`. Return empty collections or arrays directly (Item 54).
        
    - **Primitives:** Avoid `Optional<T>` for primitive types due to double-boxing (`int` -> `Integer` -> `Optional<Integer>`). Use specialized primitive optionals instead: `OptionalInt`, `OptionalLong`, and `OptionalDouble`.
        
- **Fields, Parameters & Maps:**
    
    - **Fields:** Avoid using `Optional` as class instance fields. It adds memory overhead and does not implement `Serializable`.
        
    - **Parameters:** Do not pass `Optional` as method or constructor arguments. It clutters client code; use method overloading instead.
        
    - **Maps:** Never use `Optional` as a map key or value. It creates two confusing ways to represent missing entries (`map.get(key) == null` vs. `map.get(key).isEmpty()`).
        
- **Performance Considerations:** An `Optional` requires object allocation and extra heap indirection. In extreme performance-critical loops or hot paths where memory allocations must be strictly bounded, returning `null` or a sentinel value is preferred.