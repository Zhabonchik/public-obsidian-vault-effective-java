For the sake of natural ordering of elements of your class you can Implement Comparable interface.
The following rules must be followed:
- If x < y, then y > x
- If x == y, then y == x
- If x == y and y == z then x == z
- If x > y and y > z then x > z
- Ideally, if x.equals(y) then x.compareTo(y) should be 0