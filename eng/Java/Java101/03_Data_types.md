# Data Types in Java

<br>

## 1. PDT (Primitive Data Type)

>  A type that contains the data itself

- Primitive data types => Only 8!

- The data is directly in the memory space

- The `. (dot) operator` cannot be used => why? Because it's not an address!

<br>

### 1. Boolean type

- `boolean`

  : 1bit

   (true/false) -> JAVA does not allow 0 or 1

<br>

### 2. Character type

- `char `

  : 2byte

  ex) 'a' -> only a single character is possible

   => Uses single quotation('') -> stored as ASCII code value

<br>

`+`

**byte**     ==  8bit (1 byte)  ==  -128 ~127

<br>

### 3. Integer type

- `Short`

  : 16 bit (2 byte)

-  `Int`

  : 32bit (4 byte)  => The default for integer types is Int

- `Long`

  : 64bit (8 byte)

<br>

### 4. Floating-point type

- `float`

  : 32bit (4 byte)

- `Double`

  : 64bit (8 byte)   => The default for floating-point types is Double

<br>



-> *Everything except the 8 types above is a Reference Type!!!!!*

<br><br>

## 2. Reference Type

> A type that contains an address

: Reference data type

- The memory space contains an address, and you must follow the address to find the actual data

- The `. (dot) operator` can be used!!  ex) address.

- In Reference types, you must use new for everything except String

- String can be used like a primitive type or with new!!
  - New is placed in the Heap area

  - Using it like a primitive type places it in a different area than new => this consumes less data!

    ex) String address = new String("Bitcamp");  -> when using new

    ​       String address = "Bitcamp";   -> when used like a primitive type

<br>

<br>

#### String is an immutable object!

 -> So to change String data, you need to use StringBuilder or StringBuffer

<br>

#### Buffer

= A temporary memory space

 <br>

 #### null value

= A value that explicitly indicates the absence of an address in reference types

   ex) now = null;

<br>

<br>

#### Java tries to match types based on the operator!

 ex 1)

```
 1 / 2 => 0

 1 / 2. => 0.5
```

   -> It matches the type to a floating-point type (1 becomes 1.0)

​	=> Since there is no data loss when converting from integer to floating-point, `type promotion` occurs automatically

<br>

ex 2)

```
int a = 1 + 1;   = 2

String b = "1" + "1";  = "11"

String c = 1 +1 + 1 + "1"  = "31"
```

 -> Since the result is a string, the type is declared as String

​	=> The type changes depending on what the result value is!

<br>

<br>

#### char type & int type

`char type` automatically undergoes *promotion* to `int type`!

 => but, to convert int to char, *type casting* must be done

-> why? Because there is data loss!

​     : char 2 byte    <   int 4 byte

<br>

*To go from a larger size to a smaller size, type casting is required because there is data loss!*



<br>

#### (Summary)

Larger size -> Smaller size => Data loss exists => `Type Casting`

Smaller size -> Larger size => No data loss => `Promotion`

<br><br>



#### (Type Promotion in JAVA)

![img](https://lh3.googleusercontent.com/KXOWKRk-kEyIoztoda2M7RfldyM5UmDQKPNULtwcq5_UduHG7bhd9DFu1aaVHlGdLSgs91bdaQiKdPpygaduHFRi5Ew2pF6_kIHPhOKqc4jXuRI0ZUsQ0vEI3fXAd05i7YOmpMEF)

<br>
