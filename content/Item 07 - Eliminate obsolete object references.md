Whenever a class manages its own memory it should be an alert for emory leak (nullify elements).
Another common memory leak cause - caching (use WeakHashMap if entry's lifetime is tied to its key | Cleanup jobs). 
The third memory leak cause - listeners and callbacks (Store callbacks as keys in WeakHashMap).

Garbage collector removes an unused object only if there are no references to it from other active objects.