# @Entity

- A Class that will be mapped to an actual DB Table
  - Also called an Entity Class
- By default, the Class's `Camel Case` naming is matched to table names using `Underscore(_)` naming
  - ex)
    - SalesManager.java → sales_manager
- Setter methods should not be created in Entity Classes
  - Why?
    - Because it is not clearly distinguishable in code when and where the instance values of the class should change
  - If field value changes are needed, a method with a clear purpose and intention should be added
    - ex) A function that sets the order status → setStatus (x), cancelOrder (o)
- Entity Classes basically populate values through a `constructor` and INSERT into the DB
  - When value changes are needed, a public method corresponding to the event is called to make the change
- A `Builder` can be used instead of a constructor to make it clearer which field gets which value
  - ex)
    - In the code below, the results of Example(a,b) and Example(b, a) would be different

      ```java
      public Example(String a,String b) {
        this.a=a; this.b=b;
      }
      ```

    - Using a `Builder` makes the order irrelevant
