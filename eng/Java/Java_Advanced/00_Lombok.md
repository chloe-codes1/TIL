# Lombok


<br/>



###  What is Lombok?

:  A library that allows you to easily generate boilerplate code such as Constructors, Getters/Setters, toString(), etc. through annotations when creating Model Objects like DTOs, VOs, Entities in Java

<br/>

Of course, you can easily generate them using the auto-generation feature of IDEs like Eclipse, but if a variable name changes, you have to update the corresponding functions like getters/setters as well, which is inconvenient

 -> Lombok annotations solve this inconvenience



<br/>

<br/>



### How to Use

<br/>

\- `@Data`

​     : Generates all the annotations listed below at once<br/><br/>
\- `@ToString`

​     : Generates a toString() method that prints all fields<br/><br/>
\- `@Getter`

​     : Generates Getter methods<br/><br/>
\- `@Setter`

​     : Generates Setter methods<br/><br/>
\- `@EqualsAndHashCode`

​     : Generates equals & hashcode methods <br/><br/>
\- `@NoArgsConstructor`

​	: Generates a constructor with no arguments<br/><br/>

\- `@RequiredArgsConstructor`

​    : Generates a constructor with only required arguments<br/><br/>

\- `@AllArgsConstructor`

​    : Generates a constructor with all arguments



<br/>

<br/>

### Usage Example

<br/>

![](../../kor/images/lombok최고.png)




