Instead of using tagged classes with boilerplate code introduce a class hierarchy:
abstract class for common behavior and child classes for each tag.

Benefits:
- Compile-Time safety
- Open/Closed principle
- Memory Efficiency

``` java
public abstract class Notification {  
  
    private final String message;  
  
    protected Notification(String message) {  
        this.message = message;  
    }  
  
	public String getMessage() {
		return message;
	}
  
    public abstract void send();  
}

public final class EmailNotification extends Notification {  
  
    private final String subject;  
    private final String emailAddress;  
  
  
    private EmailNotification(String subject, String emailAddress, String message) {  
        super(message);  
        this.subject = subject;  
        this.emailAddress = emailAddress;  
    }  
  
    public static EmailNotification of(String subject, String emailAddress, String message) {  
        return new EmailNotification(subject, emailAddress, message);  
    }  
  
    @Override  
    public void send() {  
        System.out.println("Sending Email to " + emailAddress + " [" + subject + "]: " + getMessage());  
    }  
}

public final class SMSNotification extends Notification {  
  
    private final String phoneNumber;  
  
    private SMSNotification(String phoneNumber, String message) {  
        super(message);  
        this.phoneNumber = phoneNumber;  
    }  
  
    public static SMSNotification of(String phoneNumber, String message) {  
        return new SMSNotification(phoneNumber, message);  
    }  
  
    @Override  
    public void send() {  
        System.out.println("Sending SMS to " + phoneNumber + ": " + getMessage());  
    }  
}

public final class PushNotification extends Notification {  
  
    private final String deviceToken;  
  
    private PushNotification(String deviceToken, String message) {  
        super(message);  
        this.deviceToken = deviceToken;  
    }  
  
    public static PushNotification of(String deviceToken, String message) {  
        return new PushNotification(deviceToken, message);  
    }  
  
    @Override  
    public void send() {  
        System.out.println("Sending Push Notification to " + deviceToken + ": " + getMessage());  
    }  
}
```