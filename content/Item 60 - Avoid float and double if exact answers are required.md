### 1. The Flaw with Binary Floating-Point Arithmetic

- **Inexact Representation:** `float` and `double` are designed for high-speed scientific and engineering calculations using IEEE 754 binary floating-point arithmetic. They deliver fast approximations, but cannot represent powers-of-ten fractions like $0.1$ or $0.01$ exactly in binary.
    
      
    
- **Error Accumulation:** Repeating simple decimal operations causes tiny rounding errors to accumulate, leading to inaccurate results.
    
      
    

### 2. The Danger in Monetary & Financial Computations

- **Currency Calculation Failures:** Performing financial operations with `float` or `double` leads to rounding bugs. For example, starting with $\$1.00$ and repeatedly subtracting $9 \times \$0.10$ leaves $\$0.09999999999999998$ instead of $\$0.10$.
    
      
    
- **Business Impact:** These errors can cause transactions to fail (e.g., incorrect balance calculations resulting in false "insufficient funds" errors) or result in illegal discrepancies in accounting systems.
    
      
    

### 3. Alternatives for Exact Calculation

1. **`BigDecimal`:** Standard Java object designed specifically for arbitrary-precision decimal arithmetic.
    
      
    
2. **Primitive Integer Types (`int` or `long`):** Hand-managed decimal scaling (e.g., tracking money in cents, micro-cents, or cents divided by $1000$).
    
      
    

### 4. Trade-Offs: `BigDecimal` vs. Primitive Integers

|**Feature**|**BigDecimal**|**Primitive Integers (int / long)**|
|---|---|---|
|**Precision & Scale**|Arbitrary precision; exact control over scale and rounding modes (e.g., `RoundingMode.HALF_EVEN`).|Fixed range ($9$ digits for `int`, $18$ digits for `long`).|
|**Syntax**|Verbose; requires method calls (`.add()`, `.subtract()`) instead of arithmetic operators.|Clean; uses native operators (`+`, `-`, `*`, `/`).|
|**Performance**|Slower; creates object instances in heap memory.|High-performance; primitive stack execution.|
|**Decimal Tracking**|Automatic.|Manual (developer must track scale, e.g., cents vs. dollars).|

> **Important `BigDecimal` Pitfall:** Always instantiate `BigDecimal` using the `String` constructor (`new BigDecimal("0.10")`), or `BigDecimal.valueOf(double)`. Never pass a `double` literal directly into the constructor (`new BigDecimal(0.10)`), as that retains the inexact floating-point value at creation.
> 
>   