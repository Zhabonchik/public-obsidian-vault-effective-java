For public classes no fields should be directly accessible. They should be accessed only through methods (getters, setters). Otherwise it breaks the encapsulation and leads to performance issues and unwanted modifications.

On the other hands it is possible to use public fields in private nested or package-private classes. Of course if they are used wisely and with caution.