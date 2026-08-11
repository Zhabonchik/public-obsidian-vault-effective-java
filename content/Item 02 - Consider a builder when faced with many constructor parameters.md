If your class' constructor consists of a bunch of parameters, especially when some of them are optional, then you should consider Builder pattern.

Advantages:
1) It is thread-safe
2) Builder allows to make the class itself immutable
3) It reduces the amount of potential constructors.

Disadvantages:
1) A bit resource-consuming in case of a strictly-optimized and performance-oriented application
2) Is an overhead when you your class has a couple of fields
   
```java
package org.example.Item2;  
  
import java.util.Objects;  
  
public class UserAccount {  
  
    private final String username;  
    private final String email;  
    private final int age;  
    private final String phoneNumber;  
    private final boolean isSubscribed;  
  
    private UserAccount(Builder builder) {  
        this.username = builder.username;  
        this.email = builder.email;  
        this.age = builder.age;  
        this.phoneNumber = builder.phoneNumber;  
        this.isSubscribed = builder.isSubscribed;  
    }  
  
    public static class Builder {  
  
        private final String username;  
        private final String email;  
        private int age = 0;  
        private String phoneNumber = "";  
        private boolean isSubscribed = false;  
  
        public Builder(String username, String email) {  
            this.username = Objects.requireNonNull(username,  "Username cannot be null");  
            this.email = Objects.requireNonNull(email,  "Email cannot be null");  
        }  
  
        public Builder age(int age) {  
            this.age = age;  
            return this;  
        }  
  
        public Builder phoneNumber(String phoneNumber) {  
            this.phoneNumber = phoneNumber;  
            return this;  
        }  
  
        public Builder isSubscribed(boolean isSubscribed) {  
            this.isSubscribed = isSubscribed;  
            return this;  
        }  
  
        public UserAccount build() {  
            validate();  
            return new UserAccount(this);  
        }  
  
        private void validate() {  
            if (!this.email.contains("@")) {  
                throw new IllegalArgumentException("Invalid email address");  
            }  
  
            if (this.age < 0) {  
                throw new IllegalArgumentException("Invalid age");  
            }  
        }  
    }  
  
    public String getUsername() {  
        return username;  
    }  
  
    public String getEmail() {  
        return email;  
    }  
}
```