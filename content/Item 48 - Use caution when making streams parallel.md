Do not parallelize streams unless you have a good reason to believe it will actually preserve correction and increase its speed.
When to use parallelizing:
- On streams over `ArrayList`, `HashMap`, `HashSet` and `ConcurrentHashSet` instances; arrays, int ranges and long ranges. It is because they can be easily split into subranges of difficult size, which makes it easy to divide work between parallel streams.
When not use it:
- If the source is from `Stream.iterate` or intermediate operation `limit()` is used.


### Final practice task
```java
public class OrderService {  
  
  
    private static final double PRICE_THRESHOLD = 200.0;  
  
    public List<String> getHighValueDeliveredOrderIds(List<Order> orders) {  
        return orders.stream()  
                .filter(o -> o.status() == DELIVERED)  
                .filter(o -> calculateTotalCost(o.items()) > PRICE_THRESHOLD)  
                .map(Order::id)  
                .toList();  
  
    }  
  
    private double calculateTotalCost(List<OrderItem> items) {  
        return items.stream()  
                .mapToDouble(item -> item.price() * item.quantity())  
                .sum();  
    }  
  
    public List<String> getTop3UniqueProductNames(List<Order> orders) {  
        return orders.stream()  
                .flatMap(order -> order.items().stream())  
                .map(OrderItem::product)  
                .distinct()  
                .sorted()  
                .limit(3)  
                .toList();  
  
    }  
  
    public Map<Status, List<Order>> groupOrdersByStatus(List<Order> orders) {  
        return orders.stream()  
                .collect(groupingBy(Order::status));  
    }  
  
    public Map<String, Double> getRevenueByCategory(List<Order> orders) {  
        return orders.stream()  
                .filter(order -> order.status() == DELIVERED)  
                .flatMap(order -> order.items().stream())  
                .collect(groupingBy(OrderItem::category, summingDouble(orderItem -> orderItem.price() * orderItem.quantity())));  
    }  
  
    public Optional<OrderItem> getMostExpensiveItem(List<Order> orders) {  
        return orders.stream()  
                .flatMap(order -> order.items().stream())  
                .max(Comparator.comparingDouble(OrderItem::price));  
    }  
  
    public boolean hasPendingFraudRisk(List<Order> orders) {  
        return orders.stream()  
                .filter(order -> order.status() == PENDING)  
                .anyMatch(order -> calculateTotalItemQuantity(order) > 50);  
    }  
  
    private int calculateTotalItemQuantity(Order order) {  
        return order.items().stream()  
                .mapToInt(OrderItem::quantity)  
                .sum();  
    }  
  
    public String getDeliveredProductCatalog(List<Order> orders) {  
        return orders.stream()  
                .filter(order -> order.status() == DELIVERED)  
                .flatMap(order -> order.items().stream())  
                .map(OrderItem::product)  
                .distinct()  
                .collect(Collectors.joining(", "));  
    }  
  
}
```