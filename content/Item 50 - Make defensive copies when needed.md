- **The Core Vulnerability:** Storing raw references to mutable objects (e.g., arrays, `java.util.Date`, mutable collections) allows external clients to bypass your class's invariants and alter internal state unexpectedly, even if fields are declared `private` and `final`.
    
- **Order of Operations (TOCTOU):** Always make defensive copies _before_ validating parameters. This prevents Time-Of-Check to Time-Of-Use (TOCTOU) attacks, where another thread modifies the parameter in the microsecond gap between validation and copying.
    
- **The `clone()` Gotcha:** Do not use `clone()` to defensively copy incoming parameters whose types can be subclassed. Untrusted subclasses could override `clone()` to leak references or compromise security. _(Note: Using `clone()` inside getter methods is acceptable if you are certain the internal object type is trusted)._
    
- **Accessors (Getters):** Return defensive copies or immutable views of internal mutable fields. Never expose direct references to mutable state in getter methods.
    
- **Exceptions & Performance:** Defensive copying can be omitted when there is mutual trust (e.g., within the same package), or when performance is critical and ownership transfer is explicitly documented—meaning any subsequent modification only affects the client, not the component's internal invariants.