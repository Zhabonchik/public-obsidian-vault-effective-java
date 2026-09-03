Streams follow the functional programming paradigm. Each stream ideally should be a pure function - it should depend only on its input parameters. In terminal operation forEach there should be no main logic, it should only report the result of computations.

- **Collectors Are Indispensable:** The majority of Item 46 focuses on `java.util.stream.Collectors`. To write streams without side effects, you must use collectors to accumulate results into collections or values rather than mutating external state inside a lambda.
- **Essential Collector Utilities to Master:**
    - **`toList()`, `toSet()`, `toCollection()`:** Standard reductions into collections.
    - **`toMap(keyMapper, valueMapper, mergeFunction)`:** Vital for mapping data. Bloch highlights using the 3-argument version with a merge function (e.g., `(oldVal, newVal) -> newVal`) to handle key collision bugs gracefully.
    - **`groupingBy()`:** The primary tool for categorizing data into groups. Bloch emphasizes combining it with downstream collectors like `counting()` or `maxBy()` for complex aggregations.
    - **`joining()`:** The idiomatic way to concatenate strings without imperative loops.
- **`forEach` as the "Least Stream-Like" Operation:** Bloch explicitly calls `forEach` imperative and un-stream-like. It should strictly be used for logging or reporting results, never for mutating an external collection (e.g., `stream.forEach(e -> list.add(e))` is a major anti-pattern).

```java
// 1. toMap: Map each employee to their unique ID (1-to-1)
Map<Integer, Employee> employeeById = employees.stream()
    .collect(Collectors.toMap(Employee::getId, emp -> emp));

// 2. groupingBy: Group employees by department (1-to-Many)
Map<Department, List<Employee>> employeesByDept = employees.stream()
    .collect(Collectors.groupingBy(Employee::getDepartment));

// 3. groupingBy with downstream collector: Count employees per department
Map<Department, Long> employeeCountByDept = employees.stream()
    .collect(Collectors.groupingBy(Employee::getDepartment, Collectors.counting()));
```