# @Transactional

<br>

### What is @Transactional?

- When @Transactional is applied to a class or method, it guarantees that methods within that scope become transactional
- Also called **declarative transaction** because it facilitates management simply by declaration without having to directly create objects
- Especially in SpringBoot, the various settings needed for declarative transactions are already configured, making it even easier to use

<br>

### Is @Transactional(readOnly=true) Really Necessary?

- It is better to use it!
- Why?
  - Even when returning queried data, it prevents `unintended data changes` in advance
    - Prevents unexpected entity registration, modification, and deletion
  - When querying an Entity in `read-only` mode, there is no need to maintain a snapshot for change detection, and there is no need to flush the persistence context, allowing for performance optimization
    - When the `readOnly=true` option is given to a transaction, the Spring Framework sets the Hibernate session flush mode to MANUAL
      - This means no flush will occur unless a flush is explicitly called!
    - Therefore, even when committing the transaction, the persistence context is not flushed, so entity registration, modification, and deletion do not work
      - Also, since the persistence context does not keep snapshots for change detection in read-only mode, performance is improved
  - With this option, CUD operations do not work, and snapshot storage and dirty checking are not performed, improving performance
    - What is `Dirty check`?
      - State change detection
      - Connected to the persistence context
        - In JPA, at the point when a transaction ends, all entity objects with changes are automatically reflected in the database
        - In JPA, when an entity is queried, a snapshot of the initial query state is created
        - At the point when the transaction ends, this snapshot is compared, and if there are differences, an Update Query is sent to the database
  - In MySQL `dual configuration (Master - Slave)`, if the DB is divided into master and slave, cases with readOnly = true will call the slave for read-only operations instead of the master
    - Depending on the situation, it can reduce the load on the DB server and provide some optimization
  - If the @Transactional(readOnly=true) annotation is present, people encountering the code can intuitively expect that the method will only perform READ operations

<br>

### Spring @Transactional vs javax @Transactional

- javax @Transactional
  - Java standard extension package
  - Provided by default in Java
- Spring @Transactional
  - Provided by org.springframework
  - Managed by the Spring Container
- Reason to use `org.springframework.transaction.annotation.Transactional`
  - It provides many Options
    - `isolation`: the underlying database isolation level
    - `noRollbackFor` and `noRollbackForClassName`: the list of Java `Exception` classes that can be triggered without triggering a transaction rollback
    - `rollbackFor` and `rollbackForClassName`: the list of Java `Exception` classes that trigger a transaction rollback when being thrown
    - `propagation`: the transaction propagation type given by the `[Propagation](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/annotation/Propagation.html)` Enum. For instance, if the transaction context can be inherited (e.g., `REQUIRED`) or a new transaction context should be created (e.g., `REQUIRES_NEW`) or if an exception should be thrown if no transaction context is present (e.g., `MANDATORY`) or if an exception should be thrown if a current transaction context is found (e.g., `NOT_SUPPORTED`).
    - `readOnly`: whether the current transaction should only read data without applying any changes.
    - `timeout`: how many seconds should the transaction context be allowed to run until a timeout exception is thrown.
    - `value` or `transactionManager`: the name of the Spring `TransactionManager` bean to be used when binding the transaction context.
