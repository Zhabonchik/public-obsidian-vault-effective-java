Ideally all the unchecked warnings should be resolved - this guarantees the correctness of your code. In case you can't eliminate some warning, but you can prove that the method is safe, then you can add **@SuppressWarnings("unchecked")** annotation and leave a justifying comment. Apply the annotation on the narrowest scope possible (method, variable).

**The Rule of Priority:**
1. Eliminate the warning by fixing the code.
2. If impossible _and_ proven safe, extract to the smallest scope (local variable).
3. Annotate with `@SuppressWarnings("unchecked")`.
4. Write a comment justifying the safety.