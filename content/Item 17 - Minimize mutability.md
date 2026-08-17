**Definition:** An immutable class is a class whose instances cannot be modified after creation.

**Five Rules of Immutability:**
1. **No mutators:** Don't provide methods that modify state.
2. **Prevent extension:** Declare the class `final` (or use private constructors with static factories).
3. **Make all fields `final`:** Clearly expresses intent and enforces immutability at compile time.
4. **Make all fields `private`:** Prevents clients from accessing or modifying raw fields.
5. **Ensure exclusive access to mutable components:** If the class references mutable objects, perform defensive copies in constructors, getters, and read-resolve methods.

**Key Advantages:**
- **Thread Safety:** Inherent safety with zero synchronization needed; instances and internals can be shared freely.
- **Failure Atomicity:** Never leaves an object in an inconsistent state on error.
- **Functional Approach:** Methods return a new instance containing the result rather than modifying the current instance (e.g., `BigInteger.add`).

**Trade-offs & Workarounds:**
- **Performance Cost:** Creating a new object for every value change can be expensive for large objects.
- **Mutable Companions:** Provide a public mutable companion class if heavy operations are needed (e.g., `StringBuilder` for `String`).
- **Static Factories:** Prefer private/package-private constructors with static factories over making the class `final` to allow internal subclassing, package isolation, and object caching.

**Rule of Thumb:** Classes should be immutable unless there’s a compelling reason to make them mutable. If a class cannot be made immutable, limit its mutability as much as possible.

```java
import java.util.List;  
  
public final class UserProfile {  
    private final String username;  
    private final Date registrationDate;  
    private final List<String> roles;  
  
    private UserProfile(String username, Date registrationDate, List<String> roles) {  
        this.username = username;  
        this.registrationDate = new Date(registrationDate.getTime());  
        this.roles = List.copyOf(roles);  
    }  
  
    public static UserProfile of(String username, Date registrationDate, List<String> roles) {  
        return new UserProfile(username, registrationDate, roles);  
    }  
  
    public String getUsername() {  
        return username;  
    }  
  
    public Date getRegistrationDate() {  
        return new Date(registrationDate.getTime());  
    }  
  
    public List<String> getRoles() {  
        return roles;  
    }  
}

// since java 14
public record UserProfile(String username, Instant registrationDate, List<String> roles) { 
	public UserProfile { roles = List.copyOf(roles); // Enforces defensive unmodifiable copy 
	} 
}

```