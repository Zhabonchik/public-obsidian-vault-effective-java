### 1. Declare Variables Where First Used & Initialize Immediately

- **Timing & Placement:** Declare local variables at the exact point they are first needed rather than at the top of a method or block.
    
      
    
- **Initialization:** Almost every local variable declaration should include an initializer. Initializing variables at the point of declaration prevents accidental use of uninitialized or stale state.
    
      
    
- **Exception (`try-catch`):** If initialization throws a checked exception, it must occur inside the `try` block. If the variable needs to be accessed outside the `try` block, it must be declared just before the `try` block.
    
      
    

### 2. Prefer `for` and `for-each` Loops Over `while` Loops

- **Scope Restriction:** `for` loops (both iteration and element-based `for-each`) allow loop variables or iterators to be declared directly in the loop header, restricting their scope strictly to the loop body.
    
      
    
- **Copy-Paste Bug Prevention:** In a `while` loop, the iterator/index variable must be declared outside the loop, causing it to linger in scope after completion. Copy-pasting a second `while` loop often leads to accidentally referencing the first loop's iterator, causing silent runtime bugs or infinite loops. A `for` loop catches this at compile time.
    
      
    
- **Idiomatic Idiom:** `for (int i = 0, n = expensiveComputation(); i < n; i++)` bounds the scope of both the loop variable `i` and the cached limit `n`.
    
      
    

### 3. Keep Methods Small and Focused

- **Single Responsibility:** If a method performs multiple distinct activities, variables used in an earlier activity remain in scope during subsequent activities, opening the door for unintended modifications.
    
      
    
- **Refactoring:** Splitting larger methods into smaller, task-specific methods ensures that local variables exist only for the brief duration of the specific subtask they serve.
    
      
    