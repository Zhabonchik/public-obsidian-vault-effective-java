- **Scope & Core Contract:** Document every exported class, interface, constructor, method, and field. Method documentation should focus on _what_ the method does rather than _how_ it works, clearly detailing preconditions, postconditions, and any side effects.
    
- **Tag Usage (`@param`, `@return`, `@throws`):**
    
    - Use `@param` for every method parameter.
        
    - Use `@return` for every non-void return value.
        
    - Use `@throws` for every thrown exception (both checked and unchecked), specifying the exact conditions that trigger it.
        
- **Summary Sentence:** The first sentence of a doc comment becomes the summary description in generated Javadoc indexes. Ensure it is a concise noun or verb phrase ending with a period and a space.
    
- **Implementation Specs (`@implSpec`):** Introduced in Java 8 to document how a method interacts with its subclasses or self-use patterns (crucial when writing `default` methods in interfaces or overridable methods in non-final classes).
    
- **Formatting Utilities:**
    
    - `{@code ...}`: Renders text in code font and automatically escapes HTML characters like `<` and `>`.
        
    - `{@literal ...}`: Escapes HTML characters without applying code font styling.
        
    - `{@index ...}`: Adds crucial terms directly into the generated Javadoc search bar.
        
- **Enums, Annotations, & Thread Safety:**
    
    - **Enums & Annotations:** Document every single enum constant and annotation member, not just the parent type.
        
    - **Thread Safety:** Every class intended for multi-threaded use must explicitly document its degree of thread safety (e.g., immutable, unconditionally thread-safe, conditionally thread-safe, or not thread-safe).


Final example:
```java
public class EventBooking {  
  
    private final String title;  
    private final Date startTime;  
    private final Date endTime;  
    private List<String> attendeeEmails;  
  
    /**  
     * Constructs an EventBooking.     *     * @param title          the title of the event  
     * @param startTime      the start time of the event  
     * @param endTime        the end time of the event  
     * @param attendeeEmails initial list of attendee emails  
     * @throws NullPointerException     if any argument is null  
     * @throws IllegalArgumentException if endTime is before startTime  
     */    public EventBooking(String title, Date startTime, Date endTime, List<String> attendeeEmails) {  
        this.title = Objects.requireNonNull(title, "Title cannot be null");  
        Objects.requireNonNull(startTime, "Start time cannot be null");  
        Objects.requireNonNull(endTime, "End time cannot be null");  
        Objects.requireNonNull(attendeeEmails, "Attendee list cannot be null");  
  
        // Item 50: Make defensive copies BEFORE parameter validation  
        this.startTime = new Date(startTime.getTime());  
        this.endTime = new Date(endTime.getTime());  
        this.attendeeEmails = new ArrayList<>(attendeeEmails);  
  
        // Item 49: Parameter validity check  
        if (this.endTime.before(this.startTime)) {  
            throw new IllegalArgumentException("End time (" + this.endTime + ") precedes start time (" + this.startTime + ")");  
        }  
    }  
  
    /**  
     * Returns the start time of the event.     *     * @return a defensive copy of the start date  
     */    public Date getStartTime() {  
        return new Date(startTime.getTime());  
    }  
  
    /**  
     * Returns an unmodifiable list of attendee emails.     *     * @return non-null list of attendee email strings  
     */    public List<String> getAttendeeEmails() {  
        // Item 54: Never return null  
        return List.copyOf(attendeeEmails);  
    }  
  
    /**  
     * Replaces current attendees with the provided collection.     *     * @param emails non-null collection of attendee email strings  
     * @throws NullPointerException if emails is null  
     */    public void setAttendees(Collection<String> emails) {  
        Objects.requireNonNull(emails, "Emails collection cannot be null");  
        this.attendeeEmails = new ArrayList<>(emails);  
    }  
  
    /**  
     * Retrieves the primary contact for the event if one exists.     *     * @return an Optional containing the primary contact email, or empty if no attendees exist  
     */    public Optional<String> getPrimaryContact() {  
        if (attendeeEmails.isEmpty()) {  
            return Optional.empty();  
        }  
        return Optional.of(attendeeEmails.getFirst());  
    }  
}
```