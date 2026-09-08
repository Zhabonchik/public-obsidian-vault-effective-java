- **Compile-Time vs. Runtime Selection:** Overloading choice is static and determined at **compile time** based on the declared static types. Overriding choice is dynamic and determined at **runtime** based on the actual object instance. This difference makes heavy overloading unintuitive.
    
- **Autoboxing and Generics Pitfalls:** Autoboxing introduced confusing ambiguities between primitive and reference overloads. For example, `List.remove(i)` invokes `remove(int index)` rather than `remove(Object element)`, requiring an explicit `(Integer)` cast to target element removal.
    
- **Lambdas & Functional Interfaces:** Avoid overloading methods to accept different functional interfaces in the exact same parameter position (e.g., `Callable` vs. `Runnable`). Compiler type-inference rules struggle with lambda target-typing, causing "ambiguous call" compile errors.
    
- **Best Practices & Alternatives:**
    
    - A safe rule of thumb is **never to export two overloads with the same number of parameters (arity)** unless their parameter types are radically different (impossible to cast to one another).
        
    - Use **distinct method names** instead of overloading (e.g., `readInt()`, `readLong()`, `readBoolean()` in `ObjectInputStream`).
        
    - Use **static factory methods** instead of overloaded constructors, allowing you to give distinct names to creation methods with identical parameter counts.