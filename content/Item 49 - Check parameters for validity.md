
**The Fail-Fast Principle:** Validate parameters at the very start of method execution to fail early. This preserves failure atomicity, prevents internal state corruption, and avoids confusing, delayed errors deeper down the call stack.

**Public API Contracts:** Document parameter restrictions on public methods using Javadoc `@throws` tags. Throw standard runtime exceptions when checks fail—typically `IllegalArgumentException`, `NullPointerException`, or `IndexOutOfBoundsException`.

**Built-in Utility Methods:** Use static helpers in `java.util.Objects` to eliminate boilerplate:
- `Objects.requireNonNull(...)` for null validation.
- `Objects.checkIndex(...)`, `checkFromToIndex(...)`, and `checkFromIndexSize(...)` for index/range validation.

**Non-Public Methods:** Validate parameters in `private` or package-private methods using assertions (`assert condition;`). Because you control all callers, invalid parameters indicate an internal bug rather than bad external input.

**Exceptions to Explicit Pre-Checks:** Skip explicit checks when:
- The check is performed **implicitly** during the core computation (e.g., `Collections.sort` comparing elements), though exception translation may be needed if the implicit check throws an unexpected exception type.
- The validation is **impractical or excessively expensive** relative to the execution cost of the method itself.