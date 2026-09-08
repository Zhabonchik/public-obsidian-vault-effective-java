- **Scope & Core Contract:** Document every exported class, interface, constructor, method, and field. Method documentation should focus on _what_ the method does rather than _how_ it works, clearly detailing preconditions, postconditions, and any side effects.
    
- **Tag Usage (`@param`, `@return`, `@throws`):**
    
    - Use `@param` for every method parameter.
        
    - Use `@return` for every non-void return value.
        
    - Use `@throws` for every thrown exception (both checked and unchecked), specifying the exact conditions that trigger it.
        
- **Summary Sentence:** The first sentence of a doc comment becomes the summary description in generated Javadoc indexes. Ensure it is a concise noun or verb phrase ending with a period and a space.
    
- **Implementation Specs (`@implSpec`):** Introduced in Java 8 to document how a method interacts with its subclasses or self-use patterns (crucial when writing `default` methods in interfaces or overridable methods in non-final classes).
    
- **Formatting Utilities:**
    
    - `{@code ...}`: Renders text in code font and automatically escapes HTML characters like `<` and `>`.
        
    - `{@literal ...}`: Escapes HTML characters without applying code font styling.
        
    - `{@index ...}`: Adds crucial terms directly into the generated Javadoc search bar.
        
- **Enums, Annotations, & Thread Safety:**
    
    - **Enums & Annotations:** Document every single enum constant and annotation member, not just the parent type.
        
    - **Thread Safety:** Every class intended for multi-threaded use must explicitly document its degree of thread safety (e.g., immutable, unconditionally thread-safe, conditionally thread-safe, or not thread-safe).