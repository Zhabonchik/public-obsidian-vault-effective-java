### 1. Strings as Value Types & Enums

- **Loss of Compile-Time Safety:** Replacing booleans, numbers, or enums with `String` hides errors from the compiler. A typo in a string value can only be caught at runtime.
    
- **Inflexible Data Manipulation:** Operations that should be native to the type (e.g., numeric comparisons or enum checks) instead require custom parsing, formatting, and string manipulation.
    

### 2. Strings as Aggregate Types

- **Delimiter Collisions:** Combining multiple data fields into a single string with a delimiter (e.g., `"Key#Value#ID"`) fails if any component naturally contains the delimiter character.
    
- **Fragile & Cumbersome Code:** Extracting individual fields requires manual string parsing, which is slow and error-prone. A simple static member class (or `record`) provides better structure, performance, and field safety.
    

### 3. Strings as Capability Keys

- **Lack of Uniqueness:** Using strings as shared tokens or capability keys (like early `ThreadLocal` implementations) living in a global namespace makes collisions inevitable.
    
- **Accidental Overwrites & Security Risks:** If two independent libraries choose the same string key (e.g., `"CLIENT_KEY"`), one will silently overwrite or expose the other's data. Unforgeable instance references should always be used as capability tokens instead.