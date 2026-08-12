Try-with-resources should be preferred to try-finally because it has the following benefits:
- Code is cleaner and clearer
- People usually forget about closing resources themselves in a finally block
- The exception history is cleaner and the original exception is not suppressed