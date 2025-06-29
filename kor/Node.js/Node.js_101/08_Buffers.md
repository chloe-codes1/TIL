# Buffers in Node.js

> Pure JavaScript is Unicode friendly, but it is not so for binary data.
>
> While dealing with TCP streams or the file system, it's necessary to handle octet streams.

<br>

- Node provides `Buffer class` which provides instances to **store raw data** similar to an **array of integers** but corresponds to a raw memory allocation outside the V8 heap.
- `Buffer class` is  a **global class** that can be accessed in an application without importing the buffer module

<br>

<br>

### 1. Creating Buffers

> Node Buffer can be constructed in a variety of ways!

<br>

#### Method 1

```javascript
var buf = new Buffer(10);
```

- Create an uninitiated `Buffer` of 10 octets

<br>

#### Method 2

```javascript
var buf = new buffer([10, 20, 30, 40, 50]);
```

- Create a `Buffer` from a given array

<br>

#### Method 3

```javascript
var buf = new Buffer('Strin')
```

- Create a `Buffer` from a given string and optionally encoding type

<br>

<br>

### 2. Writing to Buffers

<br>

#### Syntax

```javascript
buf.write(string[, offset][, length][, encoding])
```

<br>

#### Parameters

- **string**

  - `string data` to be written to buffer

- **offset**

  - `index` of the buffer to start writing at

  - default value is `0`

- **length**

  - number of bytes to write
  - defaults to `buffer.length`

- **encoding**

  - encoding to use
  - default is `utf8`

<br>

#### Return Value

: `.write()` 은 쓰여진 **octet** 의 수를 return 한다

ex)

> buffer_write.js

```javascript
buf = new Buffer(256);
len = buf.write("Buffer write method test~! ^____^")

console.log("Octets written : "+ len);
```

<br>

> Result

```shell
$ node buffer_write.js 
Octets written : 33
(node:20416) [DEP0005] DeprecationWarning: Buffer() is deprecated due to security and usability issues. Please use the Buffer.alloc(), Buffer.allocUnsafe(), or Buffer.from() methods instead.
```

<br><br>

### 3. Reading from Buffers

<br>

#### Syntax

```javascript
buf.toString([encoding][, start][, end])
```

<br>

#### Parameters

- **encoding**
  - encoding to use
  - default is `utf8`
- **start**
  - beginning index to start reading
  - defaults is to `0`
- **end**
  - end index to end reading
  - default is `complete buffer`

<br>

#### Return Value

: `toString`은 encoding 된 buffer data를 지정한 character set으로 return 한다!

ex)

> buffer_toString.js

```javascript
buf = new Buffer(26);
for (var i = 0 ; i < 26 ; i++) {
  buf[i] = i + 97;
}

console.log( buf.toString('ascii'));       // outputs: abcdefghijklmnopqrstuvwxyz
console.log( buf.toString('ascii',0,5));   // outputs: abcde
console.log( buf.toString('utf8',0,5));    // outputs: abcde
console.log( buf.toString(undefined,0,5)); // encoding defaults to 'utf8', outputs abcde
```

<br>

<br>

### 4. Convert Buffer to JSON

<br>

#### Syntax

```
buf.toJSON()
```

<br>

#### Return Value

: Buffer instance를 `JSON` 형식으로 return 한다!

<br>

ex)

> buffer_toJSON.js

```
var buf = new Buffer('Make it into JSON object');
var json = buf.toJSON(buf);

console.log(json);
```

<br>

> result

```
$ node buffer_toJSON.js 
{ type: 'Buffer',
  data:
   [ 77,
     97,
     107,
     101,
     32,
     105,
     116,
     32,
     105,
     110,
     116,
     111,
     32,
     74,
     83,
     79,
     78,
     32,
     111,
     98,
     106,
     101,
     99,
     116 ] }
```

<br>

<br>

### 5. Concatenate Buffers

<br>

#### Syntax

```
Buffer.concat(list[, totalLength])
```

<br>

#### Parameters

- **list**

  - Array List of Buffer objects to be concatenated.

- **totalLength**

  - This is the total length of the buffers when concatenated.

  <br>

#### Return Value

: `.concat()`은 Buffer instance를 return 한다

<br>

ex)

> buffer_concat.js

```
var buffer1 = new Buffer('지금은 저녁 11시 ');
var buffer2 = new Buffer('배가 고프다');
var buffer3 = Buffer.concat([buffer1,buffer2]);

console.log("buffer3 content: " + buffer3.toString());
```

<br>

> Result

```
$ node buffer_concat.js 
buffer3 content: 지금은 저녁 11시 배가 고프다
```

<br>

<br>

### Compare Buffers

<br>

#### Syntax

```
buf.compare(otherBuffer);
```

<br>

#### Parameters

- **otherBuffer**
  - 위의 syntax 예시에서 `buf`와 비교할 다른 **buffer**

<br>

#### Return Value

- `buf`과 `otherBuffer`를 비교할 때
  - 같으면 return `0`
  - sort 한 후 `otherBuffer` 가 `buf` 보다 더 앞에 오면 `1`
  - sort 한 후 `otherBuffer` 가 `buf` 보다 더 뒤에 오면 `-1`

ex)

> buffer_compare.js

```
const buf1 = Buffer.from('ABC');
const buf2 = Buffer.from('BCD');
const buf3 = Buffer.from('ABCD');

console.log(buf1.compare(buf1));
// Prints: 0
console.log(buf1.compare(buf2));
// Prints: -1
console.log(buf1.compare(buf3));
// Prints: -1
console.log(buf2.compare(buf1));
// Prints: 1
console.log(buf2.compare(buf3));
// Prints: 1
console.log([buf1, buf2, buf3].sort(Buffer.compare));
// Prints: [ <Buffer 41 42 43>, <Buffer 41 42 43 44>, <Buffer 42 43 44> ]
// (This result is equal to: [buf1, buf3, buf2].)
```

<br>

> Result

```shell
$ node buffer_compare.js 
0
-1
-1
1
1
[ <Buffer 41 42 43>, <Buffer 41 42 43 44>, <Buffer 42 43 44> ]
```

<br>

<br>

### Copy Buffer

<br>

#### Syntax

```
buf.copy(targetBuffer[, targetStart][, sourceStart][, sourceEnd])
```

<br>

#### Parameters

- **targetBuffer**
  - Buffer object where buffer will be copied.
- **targetStart**
  - Number, Optional
  - Default: `0`
- **sourceStart**
  - Number, Optional
  - Default: `0`
- **sourceEnd**
  - Number, Optional
  - Default: `buffer.length`

<br>

#### Return Value

: return 값 없음~!

<br>

ex)

> buffer_copy.js

```
var buffer1 = new Buffer('몇시에 잘까?');

//copy a buffer
var buffer2 = new Buffer(20);
buffer1.copy(buffer2);
console.log("buffer2 content: " + buffer2.toString());
```

<br>

> Result

```
$ node buffer_copy.js 
buffer2 content: 몇시에 잘까?
```

<br>

<br>

### Slice Buffer

<br>

#### Syntax

```
buf.slice([start][, end])
```

<br>

#### Parameters

- **start** − Number, Optional, Default: 0
- **end** − Number, Optional, Default: buffer.length

<br>

#### Return Value

Returns a new buffer which references the same memory as the old one, but offset and cropped by the start (defaults to 0) and end (defaults to buffer.length) indexes. Negative indexes start from the end of the buffer.

<br>

ex)

> buffer_slice.js

```
var buffer1 = new Buffer('Slice this buffer');

//slicing a buffer
var buffer2 = buffer1.slice(0,10);
console.log("buffer2 content: " + buffer2.toString());
```

<br>

> Result

```
$ node buffer_slice.js 
buffer2 content: Slice this
```

<br>
