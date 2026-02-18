# @Column

- A column of a Table
- Even without explicit declaration, all fields of a Class with the `@Entity` annotation become Columns
- Reason for use
  - Used when there are options that need to be changed beyond the default values
    - The default value for strings is VARCHAR(255), and this annotation can be used when you want to increase the size
- Options
  - `columndefinition`
    - VARCHAR: 1 to 255 characters
    - TEXT: up to 2^16
    - MEDIUMTEXT: up to 2^24
    - LONGTEXT: up to 2^32
