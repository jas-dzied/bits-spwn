# bits-spwn
A library for performing bitwise operations

# Features
bits includes 2 types: `@bitwise` and `@bitstring`.

# `@bitwise`

The `@bitwise` type is a container for all operations that can be applied to binary strings, as well as a function to 'coerce' different data types into a bit string.

# `@bitstring`

The `@bitstring` type is used to represent a series of bits. The type also has extra methods attached to it that do the same thing as `@bitwise::[chosen method]` with `self` passed in as the first argument. E.g: `@bitstring::new("100").xor("010")`.

# Argument typing

All arguments in the library can be of any type that either can be directly converted to a `@bitstring` with `{type} as @bitstring` or convert to any other type that can be converted to a bitstring. This means you can allow your custom types to be passed in as arguments. When doing this, it is recommended to convert to `@string`, as that is the data type internally used for storage. This can be seen in the code showcase below.

# Showcase

### Code

```
bits = import bits

$.print(bits.bitwise::and("10110", "01101"))
$.print(bits.bitwise::or("10110", "01101"))
$.print(bits.bitwise::xor("10110", "01101"))
$.print(bits.bitwise::not("10110"))

$.print()

$.print(bits.bitwise::lshift("010"))
$.print(bits.bitwise::rshift("010"))
$.print(bits.bitwise::lrotate("100"))
$.print(bits.bitwise::rrotate("001"))

$.print()

op1 = @bitstring::new("101")
op2 = @bitstring::new(52)
$.print(op1)
$.print(op2)

$.print()

$.print(op1.and(op2))
$.print(op1.or(op2))
$.print(op1.xor(op2))
$.print(op1.not())

$.print()

$.print(op1.lshift())
$.print(op1.rshift())
$.print(op1.lrotate())
$.print(op1.rrotate())

$.print()

type @custom_type
impl @custom_type {
    _as_: (self, _type: @type_indicator) {
        if _type == bits.bitstring {
            return self.prop
            // return bits.bitstring::{value: self.prop}
            // ^ both of these work
        }
    }
}
$.print(bits.bitwise::and(@custom_type::{prop: "0011"}, "0101"))

$.print(bits.bitwise::convert("1111"))
$.print(bits.bitwise::convert(76))
$.print(bits.bitwise::convert(true))
```

### Output

```
———————————————————————————

@bitstring::{value: '00100'}
@bitstring::{value: '11111'}
@bitstring::{value: '11011'}
@bitstring::{value: '01001'}

@bitstring::{value: '100'}
@bitstring::{value: '001'}
@bitstring::{value: '001'}
@bitstring::{value: '100'}

@bitstring::{value: '101'}
@bitstring::{value: '110100'}

@bitstring::{value: '000100'}
@bitstring::{value: '110101'}
@bitstring::{value: '110001'}
@bitstring::{value: '010'}

@bitstring::{value: '010'}
@bitstring::{value: '010'}
@bitstring::{value: '011'}
@bitstring::{value: '110'}

@bitstring::{value: '0001'}
@bitstring::{value: '1111'}
@bitstring::{value: '1001100'}
@bitstring::{value: '1'}
———————————————————————————
```
