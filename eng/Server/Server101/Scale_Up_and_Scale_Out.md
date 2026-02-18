# Scale Up and Scale Out

> Reference: [library.gabia.com](http://library.gabia.com/contents/infrahosting/1222)

<br>

<br>

## Two Methods for Server Expansion - `Scale Up`, `Scale Out`

<br>

When more server capacity and performance are needed, you can expand the system using two methods: **Scale Up** and **Scale Out**

<br>

### 1. Scale Up

- Scale-up means increasing the server's own **performance** by adding CPU or RAM to the server, or replacing it with higher-performance components or a server
  - In other words, it means upgrading from the existing server to a higher-performance server
    - Also called *"Vertical Scaling"*
- Since all data is processed on a single server, it is a suitable method for DB Servers where data updates occur frequently

![Screen Shot 2020-09-22 at 3.12.23 PM](../../kor/images/Screen Shot 2020-09-22 at 3.12.23 PM.png)

<br>

#### Problems with Scale-up

- Since all the load is concentrated on a single server, there is a risk of being significantly affected in the event of a failure

- The problem of **scalability limitations** of the storage controller
- **Migration** costs that arise when performance & capacity expansion limits are reached and a new system needs to be added

<br>

<br>

### 2. Scale Out

- A method of improving processing capability by increasing the number of servers with the same or similar specifications as the existing server
  - Also called *"Horizontal Scaling"*
- Expansion is somewhat more flexible compared to **Scale-up**
- Since there are multiple servers, **load balancing** must be implemented to evenly distribute the load across each server

![Screen Shot 2020-09-22 at 3.20.20 PM](../../kor/images/Screen Shot 2020-09-22 at 3.20.20 PM.png)

<br>

#### Advantages of Scale Out

- Even if one server goes down due to a failure, service can continue to be provided through other servers

<br>

#### Problems with Scale Out

- Since all servers must have the same data, it is a suitable method for **web servers** where data changes are infrequent

- Difficulty in **designing** and **implementing** `Parallel Computing`
  - There are fundamentally parts that need to be serialized (single processing),
  - There are bandwidth and synchronization issues, and
  - Performance does not simply increase as cores increase; **bandwidth** increases with the number of cores, potentially causing delays

<br>

<br>

### Wrap-up

- The appropriate method should be adopted depending on the situation
  - ex)
    - When heavy **traffic** occurs due to **increased visitors**, `Scale-out` is more effective and also cheaper
    - For **OLTP (Online Transaction)** that requires frequent database updates, `Scale-up` is more effective
