If x.equals(y) returns true, then their hash codes must be equal. If x.equals(y) returns false, their hash codes are not obligatory different, but they better be.

Use significant fields from equals() to count hash code. Don't use fields for computing hash code that are not used in equals().

If an object is immutable and its hash code calculation is expensive, then stick to hashing the result on creation and returning the stored value. Also lazy-initialization may be used: compute the stored hash code on the first call, then return the stored value.