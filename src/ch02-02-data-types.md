# Data Types

Cairo has the following types:
* felt

    In Cairo when you don’t specify a type of a variable/argument, its type is a field element (represented by the keyword `felt`). In the context of Cairo, when we say “a field element” we mean an integer in the range -P/2 < x < P/2 
 where 
 is a very large (prime) number (currently it is a 252-bit number, which is a number with 76 decimal digits). When we add, subtract or multiply and the result is outside the range above, there is an overflow, and the appropriate multiple of P
 is added or subtracted to bring the result back into this range (in other words, the result is computed modulo P).

    The most important difference between integers and field elements is division: Division of field elements (and therefore division in Cairo) is not the integer division you have in many programming languages, where the integral part of the quotient is returned (so you get `7 / 3 = 2`). As long as the numerator is a multiple of the denominator, it will behave as you expect (`6 / 3 = 2`). If this is not the case, for example when we divide `7/3`, it will result in a field element `x` that will satisfy `3 * x = 7`. It won’t be `2.3333` because x has to be an integer. If this seems impossible, remember that if `3 * x` is outside the range -P/2 < x < P/2 
, an overflow will occur which can bring the result down to 7. It’s a well-known mathematical fact that unless the denominator is zero, there will always be a value x satisfying `denominator * x = numerator`.
* multiple integer type

    Multiple integer types are available in the core library: `u8`, `u16`, `u32`, `u64`, `u128`, and `u256`. Even though they rely on the basic type felt under the hood, it is safer to use them if the context is appropriate. They support arithmetic operators, meaning that you can, for example, sum them with `let sum = 1_u128 + 2_u128`. These operators automatically check for overflows and panic if one is detected. This greatly improves the clarity of the code compared to using functions for basic arithmetic operations.

    ```
    fn main() -> u128 {
        let _2e32 = 4294967296_u128;
        _2e32 * _2e32 * _2e32 * (_2e32 - 1_u128) // ok
        _2e32 * _2e32 * _2e32 * _2e32 // panic because it overflows
    }
    ```
* structs
* unnamed tuple
* named tuplep