# Microservices Architecture Style

> Let's learn about microservices architecture
>
> References: [microsoft docs](https://docs.microsoft.com/ko-kr/azure/architecture/guide/architecture-styles/microservices), [aws docs](https://aws.amazon.com/ko/microservices/)

<br>

<br>

### What are Microservices?

- Microservices are **small**, **independent**, and **loosely coupled**
  - A single small development team can write and maintain them
- Each service is a **codebase** that a small development team can manage
- Services can be **deployed independently**
  - A team can update an existing service without rebuilding and redeploying the entire application
- A service must maintain its own data or external state
  - This is the difference from the traditional model where a separate data layer handles **data persistence**!
- Services communicate with each other using well-defined APIs
  - Internal implementation details of each service are hidden from other services
- Services do not need to share the same technology stack, library, or framework

<br>

<br>

### Benefits of Microservices

- #### Agility

  - Since they are deployed independently, it is easier to manage bug fixes and releases

- #### Focused, Small Teams

  - Microservices are small enough that a single feature team can build, test, and deploy them
    - Small teams have high agility!

- #### Small Code Base

  - In monolithic applications, code dependencies tend to become tangled over time, so adding new features requires modifying code in many places
    - However, microservices architecture does not share code or data stores, so dependencies are minimized, making it easy to add new features

- #### Mix of Technologies

  - Teams can appropriately use a mix of technology stacks and choose the best technology for their service

- #### Fault Isolation

  - Even if an individual microservice becomes unavailable, if upstream microservices are designed to handle failures properly (e.g., implementing circuit breaking), it will not disrupt the entire application

- #### Scalability

  - Services can be scaled independently, allowing the scaling of subsystems that require more resources without scaling the entire application

- #### Data Isolation

  - Schema updates are much easier to perform because only a single microservice is affected
    - However, in monolithic applications, schema updates can be very difficult!
      - Because various parts of the application can all affect the same data, making schema changes risky!

<br>

<br>

### Challenges of Microservices

- #### Complexity

  - A microservice application has more moving parts than an equivalent monolithic application
    - Each individual service is simpler, but the system as a whole is more complex

- #### Difficulty of Governance

  - While the distributed approach to building microservices has advantages, it can also create problems
  - The large number of languages and frameworks used can make application **maintenance** difficult
    - Therefore, it is good to apply some standards to the project!
      - ex) Cross-cutting features like **logging**

- #### Network Congestion & Latency

  - Using many small, granular services can increase inter-service communication
  - Also, if the **dependency chain** of services (service A calls B, B calls C, and so on...) becomes too long, additional latency issues can arise
    - Therefore, APIs must be designed carefully!

- #### Data Integrity

  - Each microservice manages its own data persistence
    - Therefore, data consistency can become a problem

- #### Versioning

  - Service updates must not break dependent services
  - Since multiple services can be updated at any time, **compatibility issues** can arise if not designed carefully
