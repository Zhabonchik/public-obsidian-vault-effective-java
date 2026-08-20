As well as generic classes, generic methods are more preferable since they deprive clients of obligation to cast objects.

Thanks to type inference callers rarely need to pass explicit type arguments (writing `Union.union(set1, set2)` instead of `Union.<String>union(set1, set2)`). The compiler infers the types automatically.

**Idioms to Know:**
- Generic Singleton Factory: Reuses one stateless instance across varying parameterized types.
- Recursive Type Bounds: Uses `<T Comparable<T extends>>` to enforce natural ordering constraints.