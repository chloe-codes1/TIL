# Java Loops & Conditional Statements

<br>

<br>

## Conditional Statements

<br>

### if statement

: An if statement tells the program that it must carry out a specific piece of code if a condition test evaluates to true

```java
if( condition ) {
    statement;
} else{
    statement
}
```

<br>

### switch statement

- a multi-way branch **statement**.
- provides an easy way to dispatch execution to different parts of code based on the value of the expression

```java
switch(argument value) { // Not a conditional expression, but an argument value!

 // -> Only data types that can be promoted to int can be used as the argument value!

  // ex) Integer types (byte, short, int), character type (char)



 case condition value 1:     // => It's a colon(:), not a semicolon(;)!!!!!

  statement; // -> Statement to be executed when the conditional expression result matches the condition value

break;  // => break must be included for proper operation

 case condition value 2:

  statement;

break;

case condition value 3:

  statement;

break;

case condition value 4:

  statement;

break;

 Default:  // => default is for exiting when none of the conditions match!

  statement;
```

<br><br>

## Loops

<br>

### for loop

- A for loop is divided into three parts, an initialization part, a conditional part and an increment part
- You should sett all initial values in the initialization part of the loop.
- A true from the condition part will execute subsequent statements bounded by {} brackets. A false from the condition part will end the loop.
- For each loop the increment part will be executed.

```java
for (initialization ; condition ; increment) {

 statement 1;

 statement 2;

 ....

}
```

<br>

### Nested for loop

```java
for (initialization 1 ; condition 1 ; increment 1) {

 for (initialization 2 ; condition 2 ; increment 2) {

  statement 2

  }

 statement 1;

}

statement 3;
```

<br>

### Enhanced for loop

: The enhanced for loop can be used to loop over arrays of any type as well as any kind of Java object that implements the java.lang.Iterable interface.

```java
for ( type variableName : array or collection) {

 // statements to repeat

}
```

<br>

### while loop

: Compare first, then process

 -> The conditional expression cannot be omitted! To make the condition always true, use true

```java
while (condition ) {

 statement; -> Statements to be repeated while the condition evaluates to true

}
```

<br>

### do ~ while loop

: Executes at least once even if the condition is not met

```java
do {

 statement;

} while (condition);
```

<br><br>

### break statement

: A control statement that exits the loop containing the break

 -> The break statement exits the nearest loop!

```java


for (initialization ; condition ; increment) {



 for(initialization ; condition ; increment){

  statement;

  break;   //====> Since it is used in the inner for loop, it only exits the inner for loop

 }

}
```

<br>

<br>

### continue statement

: Used when you want to skip certain statements

 -> When continue is encountered, the statements below continue are not processed, and it moves to the increment expression for the next iteration (if there is no increment expression, it moves to the condition!)

<br>

<br>

#### Difference between break and continue statements

 : Whether or not you exit the loop!

 -> The continue statement does not exit the loop; instead, it moves to the loop's conditional expression for the next iteration!

<br>

<br>

#### The return statement terminates the function itself
