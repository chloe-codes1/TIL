# What is Cache?

> Let's learn about Cache
>
> References: [jehovah's brunch](https://brunch.co.kr/@jehovah/20)

<br>

<br>

## What is Cache?

- A space that stores data that has been read once in a **temporary space**,
  - so that the next time it is read, the result can be returned **quickly**
    - When the same request comes in multiple times, the **Cache Server** returns the result directly, reducing the load on the DB
- By utilizing the **locality** that appears when a program is executed, content that was used from memory or disk is **stored** and **managed** in a quickly accessible location so that it can be quickly referenced when needed next time
  - In other words, it utilizes the concept that *data that has been used is likely to be used again*
    - Data that is likely to be used again is stored in a **faster** accessible storage!

<br>

<br>

## Usage Patterns

<br>

### Cache Usage Pattern 1 - Data Cache

- When a Client sends a request to a web server, the web server checks whether data exists in the **Cache** before fetching data from the **DB**
  - **If data exists in the Cache server,**
    - The data is returned to the client from the cache without requesting it from the DB
      - This is called a `Cache hit`
  - **If data does not exist in the Cache server,**
    - This is a `Cache miss` situation, and the data is requested from the DB
      - The DB returns the data the user wants,
      - The Web Server saves the returned data in the **cache** for future use and then returns it to the client
        - Afterward, when the same request comes in, the data stored in the **cache** can be returned, resulting in a `Cache hit`

- This structure is the same as the **CDN service** that caches **Static assets**
  - CDN services like `Amazon CloudFront` cache data from the origin (e.g., Amazon S3) that holds the original data,
  - so that the next time the same request comes in, the result can be returned immediately without requesting the origin data

<br>

### Cache Usage Pattern 2 - When Simultaneous Writes Occur

- When **simultaneous writes** occur, write requests can suddenly flood the DB and potentially crash it; in this case, Cache can be utilized
  - The Client sends a write request to the web server,
    - and the web server writes the data to the **cache** and immediately returns the result
  - Cache typically uses **memory**, so the speed is quite fast
    - Separately running **worker servers**
      - fetch data from the **cache server**,
      - perform the work,
      - and write the results to the DB
    - By doing this, the DB can process **transactions** sequentially

<br>

<br>

### Terms

- `Cache hit`
  - When the data you want to reference exists in the cache
- `Cache miss`
  - When the data you want to reference does not exist in the cache
