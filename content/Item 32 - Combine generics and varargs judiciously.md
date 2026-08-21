Varargs example:
```java
public <T> List<T> flatten(List<? extends T>... lists);
```
During compilation varargs are translated into an array. For the case above -> List[].
We can consider varargs method as save in 2 cases:
- We do not add any elements to the varargs array
- We do not expose a reference to this array to clients

The bad example is the following:
```java

void main() {
	String[] strings = chooseTwo("No", "Hello", "World");
}

public static <T> T[] chooseTwo(T arg1, T arg2, T arg3) {
	return toArray(arg2, arg3);
}

private static <T> T[] toArray(T... args) {
	return args;
}
```
What will be the problem? In compile time in choseTwo() method will be translated into Object[]. So, toArray() will receive Object arg2, Object arg3 and thus return the Object[]. Since arrays are reifiable there will me the following cast in main:
```java
String[] strings = (String[]) Object[];
```
Since the Object[] is not a subtype of String[], there will be a ClassCastException. Because for reifiable types the information of the actual object type is stored in a header on heap.

The safe option would be the following:
```java
void main() {
	List<String> strings = chooseTwo("No", "Hello", "World");
}

public static <T> List<T> chooseTwo(T arg1, T arg2, T arg3) {
	return List.of(arg2, arg3);
}
```
Why so? Because Lists are non-refiable and the info in header for new ArrayList\<String\> and new ArrayList\<Integer\> will be the same: ArrayList.

And so in main we will have:
```java
void main() {
	List<String> strings = (List) chooseTwo("No", "Hello", "World");
	String a = (String) strings.get(0);
}
```
Because the string.get(0) holds an instance of String, which is reifiable, the casting type and the type in header on heap will be the same and no error will be thrown.