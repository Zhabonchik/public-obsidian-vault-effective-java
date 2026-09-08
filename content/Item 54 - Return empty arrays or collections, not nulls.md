- **The Core Issue:** Returning `null` instead of an empty collection or array forces every client caller to write defensive null checks (`if (items != null)`). Forgetting a check leads directly to a `NullPointerException`. Returning an empty collection or array simplifies client code and eliminates an entire class of bugs.
    
- **The Performance Myth:** The common argument for returning `null` is to avoid the cost of allocating empty objects. However, modern JVM allocations are extremely cheap, and premature optimization here degrades API usability for negligible gain.
    
- **Zero-Allocation Solutions:** If allocation overhead is a legitimate performance concern, you can completely eliminate it without returning `null`:
    
    - **For Collections:** Return immutable empty collection singletons like `Collections.emptyList()`, `Collections.emptySet()`, or `Collections.emptyMap()`.
        
    - **For Arrays:** Return a reusable, zero-length static array constant (e.g., `private static final String[] EMPTY_ARRAY = new String[0];`).