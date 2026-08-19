**Generic type** is a class or an interface followed by one or mare of its parameters in declaration (List\<E\>).
A generic type with concrete parameters is called **parameterized** (List\<String\>).
A generic type without any parameters (just its name) in arrow braces is called a **raw type** (List).

Raw types have been preserved for backward compatibility in Java 5. If we use Raw types, compiler puts invisible typecasts but bypasses compile-time checks on insertion which result into runtime ClassCastException later.

Suppose the following:
```java
List<String> stringList = new ArrayList<>();

List rawList = stringList; // this is allowed, since List<String> is a subtype of List

List<Object> parameterizedList = stringList; // not allowed! List<String> is not a subtype of List<Object>
```

If you want to use a generic type but you don't know or don't care which type the actual parameter is, you can use an **unbounded wildcard type**.
You can put only null to a Collection\<?\>, but you can get elements from it.

```java
List<String> stringList = new ArrayList<>();
stringList.add("Hello");

List<?> wildcardList = stringList;
wildcardList.getFirst(); // allowed
wildcardList.add(null); // allowed
wildcardList.add("World"); // not allowed
```

This is also useful for using with **instanceof** operator:
```java
if (o instanceof Set) {
	Set<?> set = (Set<?>) o;
	...
}
```

| Term                    | Example                              |
| ----------------------- | ------------------------------------ |
| Parameterized type      | List\<String\>                       |
| Actual type parameter   | String                               |
| Raw type                | List                                 |
| Generic type            | List\<E\>                            |
| Formal type parameter   | E                                    |
| Unbounded wildcard type | List\<?\>                            |
| Bounded type parameter  | List\<E extends Number\>             |
| Recursive type bound    | List\<T extends Comparable\<T\>\>    |
| Bounded wildcard type   | List\<? extends Number\>             |
| Generic method          | static \<E\> List\<E\> asList(E[] a) |
| Type token              | String.class                         |
