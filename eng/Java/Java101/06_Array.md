# Array in Java

<br>

## Understanding Arrays

### What is an Array?

- A way to handle multiple variables of the same type as a single group

- An array is a data type that allows handling memory spaces of the same type under a single name.

- A variable accompanied by a position index

  => A position index always accompanies it

- Since arrays are also Classes, methods can be used
- Once the size of an array is set, it cannot be resized!

<br>

### Disadvantages of Arrays

- The `size` `cannot be changed`
  - If expansion is needed, a new array must be created and copied
  - If the array is created with a large size to improve execution speed, memory is wasted
- `Adding/removing` `non-sequential data` takes a lot of time
  - Adding data sequentially and removing the last data is very fast, but
    - Adding/removing values in the middle of the array takes a long time

<br>

### Array vs ArrayList & LinkedList

- Arrays have these disadvantages, and `ArrayList`, which `implements List using arrays`, also has the same problems
  - The data structure designed to address these issues is `LinkedList`
    - While arrays have all data existing `contiguously`,
    - `LinkedList` consists of `non-contiguous` data connected to each other

<br>

## Using Arrays

### 1. Declaration

  type[] variableName;

ex)

```java
// ver1)
int[] scores;

// ver2)
int scores[];
```

<br>

### 2. Creation

  variableName = new type[length];

ex)

```java
int [] nums = new int [5];
```

 -> Array declaration and creation done at once

  \* *The length of an array must be a positive integer (including 0) within the int range!*

<br>

### 3. Initialization

   : Since arrays are automatically initialized to the default value of their type upon creation, you don't need to initialize them separately before use, but to store desired values, you must assign values to each element

ex)

```java
int num;
```

- Create a memory space called num in the Stack area
- And integers will be stored here

<br>

```java
int [] nums = new int[5] ;
```

The moment an array is declared, it becomes a `reference type`!!!

- Create an address called nums in the Stack area

- Since it's new, create 5 rooms of int type in the Heap area
  - Since it's in the heap, JVM manages it
  - Then, each of the 5 rooms undergoes default initialization to 0 since they are int type, by the JVM

- Once created this way, resizing is not possible

- Guaranteed to receive contiguous memory allocation

<br>

```java
int [] nums.length ;
```

- What is the size of the nums array?

<br>

```java
String name;
```

- Create a memory space called String in the Stack area

- And addresses will be stored here

<br>

```java
String[] names = new String[5];
```

- reference type!

- Each of the 5 rooms undergoes default initialization to null by the JVM

<br>

```java
names[0] = "Hong Gildong";
```

- The address pointing to "Hong Gildong" in the code table area is stored in room 0 of names

<br>

### 4. Copying Arrays

```java
System.arraycopy(arg0, arg1, arg2, arg3, arg4);
```

**Parameters :**

- source_arr : array to be copied from  (original array)

- sourcePos : starting position in source array from where to copy

- dest_arr : array to be copied in  (destination array)

- destPos : starting position in destination array, where to copy in

- length : total no. of components to be copied.  (size of the original array)

<br>

### 5. Two-Dimensional Array

- An array made by collecting addresses of one-dimensional arrays

- A two-dimensional array stores the addresses of data pointed to by one-dimensional arrays

- When an array is created, each element is automatically stored with the default value of the element type

- Since a 2D array consists of `rows` and `columns`, indexes exist for both rows and columns
  - Row index range = 0 to row length - 1
  - Column index range = 0 to column length - 1

<br>

#### Length of a Two-Dimensional Array

```java
int [ ] [ ] score = [5][3];

score.length //==> 5
//-> length of the array referenced by score

score[0].length //==> 3
//-> length of the array referenced by score[0]
```

<br>

#### String to char array

: `.toCharArray();`

```java
import java.util.Arrays;

public class JavaStringToCharArray {

 public static void main(String[] args) {
  String str = "Hi Java";

  // get char at specific index
  char c = str.charAt(0);

  // Character array from String
  char[] charArray = str.toCharArray();

  System.out.println(str + " String index 0 character = " + c);
  System.out.println(str + " String converted to character array = " + Arrays.toString(charArray));

 }

}
```

<br>

#### (String ...) vs String[]

1. (String ...) means you can add as much String param as you want

2. String[] is one parameter which is an array of strings.

<br>

#### Running args in Oracle

![img](https://lh3.googleusercontent.com/uGqQh0xF6AbgCvfISK3_liROQRWTzf6W_F__F1W-tJnGakIAnExSAP-kiAUABWS66CIzSviOy-k6xPS-z9tXuM9kNFFn1hZ70fO3kdcDrb7NV2hxCHg_XSs6qBczN-yfYJhZsKZQ)

<br>
