Make program elements as hidden as possible (within the logic):
- Only classes that are part of API should be made public.
- No field should be public.
- Public static final fields should be of primitive or unmodifiable type.
- It is possible to make unmodifiable public static final copies of private static fields

Access level: public -> protected -> default -> private.
