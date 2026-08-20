Follow the PECS rule: producers extend, consumers super. Comparators and Comparable are consumers.
```java
public static <T extends Comparable <? super T>> T max(List<? extends T> list);
```

- **Producer (`? extends T`):** Use when an input parameter strictly _provides_ data to your method (reading elements out).
- **Consumer (`? super T`):** Use when an input parameter strictly _consumes_ data (writing elements into it, or evaluating elements via `Comparable`/`Comparator`).
- **Rule for Return Types:** Never use wildcard types as return types. They force callers to deal with wildcards in their own code, ruining API ergonomics.