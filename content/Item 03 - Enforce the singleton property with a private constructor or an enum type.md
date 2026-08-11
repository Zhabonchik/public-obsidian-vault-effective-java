In order to create a singleton class go for a private constructor or a single enum.

With private constructor you create a static final instance variable of your class and initialize it with a private constructor once. Then you can either make the field public or introduce getInstance() method (Static factory). 

```java
public class MyClass {
	
	// simplier and more clear
	public static final MyClass INSTANCE = new MyClass();
	//private static final MyClass INSTANCE = new MyClass();
	
	private MyClass() {...}
	
	public void doSomething() {...}
	
	
	// can be modified to return new objets or used as method reference
	/*public static MyClass getInstance() {
		return INSTANCE;
	}*/
}
```
In case of serialization you will have to make sure the class is properly serialized making all fields transient and implementing readResolve() method.

The best approach will be a single enum, that already handles serialization properly:
```java
package org.example.Item3;  
  
import java.util.Map;  
import java.util.concurrent.ConcurrentHashMap;  
  
public enum AppSettings implements SettingsManager {  
    INSTANCE;  
  
    private final Map<String, String> settings = new ConcurrentHashMap<>();  
  
    @Override  
    public String getSetting(String key) {  
        return settings.get(key);  
    }  
  
    @Override  
    public void setSetting(String key, String value) {  
        settings.put(key, value);  
    }  
  
}
```
