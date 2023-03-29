# Data Types

Cairo has the following types:
* ## Felt

    In Cairo when you don’t specify a type of a variable/argument, its type is a field element (represented by the keyword `felt`). In the context of Cairo, when we say “a field element” we mean an integer in the range -P/2 < x < P/2 
 where 
 is a very large (prime) number (currently it is a 252-bit number, which is a number with 76 decimal digits). When we add, subtract or multiply and the result is outside the range above, there is an overflow, and the appropriate multiple of P
 is added or subtracted to bring the result back into this range (in other words, the result is computed modulo P).

    The most important difference between integers and field elements is division: Division of field elements (and therefore division in Cairo) is not the integer division you have in many programming languages, where the integral part of the quotient is returned (so you get `7 / 3 = 2`). As long as the numerator is a multiple of the denominator, it will behave as you expect (`6 / 3 = 2`). If this is not the case, for example when we divide `7/3`, it will result in a field element `x` that will satisfy `3 * x = 7`. It won’t be `2.3333` because x has to be an integer. If this seems impossible, remember that if `3 * x` is outside the range -P/2 < x < P/2 
, an overflow will occur which can bring the result down to 7. It’s a well-known mathematical fact that unless the denominator is zero, there will always be a value x satisfying `denominator * x = numerator`.
* ## Boolean
    Boolean are natively supported in cairo. It can then be used in if logic for example:
    ```
    let is_morning = true;
    if is_morning {
        debug::print_felt('Good morning!');
    }
    ```

* ## String 
    You can put char or string inside felts too!
    ```
    let mut my_first_initial = 'C';
    ```
* ## Multiple integer type

    Multiple integer types are available in the core library: `u8`, `u16`, `u32`, `u64`, `u128`, and `u256`. Even though they rely on the basic type felt under the hood, it is safer to use them if the context is appropriate. They support arithmetic operators, meaning that you can, for example, sum them with `let sum = 1_u128 + 2_u128`. These operators automatically check for overflows and panic if one is detected. This greatly improves the clarity of the code compared to using functions for basic arithmetic operations.

    ```
    fn main() -> u128 {
        let _2e32 = 4294967296_u128;
        _2e32 * _2e32 * _2e32 * (_2e32 - 1_u128) // ok
        _2e32 * _2e32 * _2e32 * _2e32 // panic because it overflows
    }
    ```

    If you try to sum two integers and the result is bigger than the biggest integer of this type, you'll get a compilation error.

    You can convert integers to felts using the `.into()` method. Make sure that you imported the `Into` trait.

    You can convert felts to integers using the `.try_into()` method. Make sure that you imported the `TryInto` trait.
    
    This method will return an `Option` type, so you'll need to unwrap it. To use the `unwrap()` method, you'll need to import the `OptionTrait` trait.

    #### Type literals

    Numeric literals are fixed values for numbers, such as `1`, `2`, or `3`. These literals are `felts` by default, but using a suffix `_<type>` we can specify a specific type for our literal, such as `uint128` . You can use type literals as function arguments, improving code clarity and readability compared to the previous version of Cairo.

    ```let my_u128 = 1_u128;```
* ## Struct

    structs are a custom data type that provides a way to group values, defining a single entity that represents a collection of related values. We can define methods that can operate on the struct using a combination of impls and traits.
    In order to destructure a struct into multiple variables, you can use the following syntax: `let Point{x: a, y: b} = origin;`
    ```
    #[derive(Copy, Drop)]
    struct Point { x: felt, y: felt }

    fn main() -> felt {
        let mut origin = Point { x: 0, y: 0 };
        let p = Point { x: 1, y: 2 };
        let x = origin.x;
        let Point{x: a, y: b } = origin;
        a // returns 0
    }
    ```
* ## Tuple
    A tuple type is defined similarly to a tuple expression. For example, given two types `a` and `b`, the type `(a, b)` represents a tuple that consists of an element of type a and an element of type b. For example `(felt, felt)` may be used to represent a (2-dimensional) point.

    #### Named tuple
    Cairo also supports named tuples, for example `(x: felt, y: felt)` represents a tuple similar to `(felt, felt)` except that the two items are named x and y, respectively.

    #### User-defined type aliases
    You can give a new alias for a type as follows:

    ```using Point = (x: felt, y: felt);```
    Note that Point is not a new type in this case – it is only an alias to (x: felt, y: felt). You can use Point as an alias for this type.

    For example, you may replace

   ``` local pt: (x: felt, y: felt) = (x=2, y=3);```

    with:

    ```local pt: Point = (x=2, y=3);```