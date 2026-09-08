- **Naming & API Scope:** Choose clear, descriptive names that follow standard Java conventions and align with the surrounding package. Keep APIs focused and lean—avoid adding convenience methods unless they are heavily used, as every method requires testing, documentation, and maintenance.
    
- **Parameter Count (Rule of Four):** Aim for four parameters or fewer. Long parameter lists are difficult to read and error-prone. To reduce parameter count:
    
    - **Split methods:** Break a complex method into multiple smaller, orthogonal methods.
        
    - **Helper classes:** Group related parameters into dedicated helper classes (often static inner classes).
        
    - **Builder pattern:** Adapt the Builder pattern for method calls with many parameters, especially when several are optional.
        
- **Parameter Types (Interfaces over Classes):** Prefer interface types over concrete classes for parameters (e.g., pass `Map` instead of `HashMap`). This maximizes flexibility for callers and avoids forcing redundant data type conversions or method overloads.
    
- **Booleans vs. Enums:** Favor two-element `enum` types over `boolean` parameters. Enums make call sites self-documenting (e.g., `TemperatureScale.CELSIUS` instead of `true`) and can easily accommodate additional options in the future without breaking existing method signatures.