In Java arrays are **covariant**, which means that if b is subtype of a, then b[] is a subtype of a[]. Generics are invariant, though.
```java
Object[] o = new Long[1]; // this is valid
o[0] = "hello"; //will compile but throw ArrayStoreException in runtime
```
Secondly, arrays are **reified**, which means that arrays provide runtime-safety, but not the compile-time. For Generics it's vice-versa since in runtime type erasure comes into play.

Generally speaking, it's impossible to mix arrays with Generics, that is why if you need to use generics with arrays - use Lists instead.
