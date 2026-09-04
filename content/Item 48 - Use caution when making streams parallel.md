Do not parallelize streams unless you have a good reason to believe it will actually preserve correction and increase its speed.
When to use parallelizing:
- On streams over `ArrayList`, `HashMap`, `HashSet` and `ConcurrentHashSet` instances; arrays, int ranges and long ranges. It is because they can be easily split into subranges of difficult size, which makes it easy to divide work between parallel streams.
When not use it:
- If the source is from `Stream.iterate` or intermediate operation `limit()` is used.