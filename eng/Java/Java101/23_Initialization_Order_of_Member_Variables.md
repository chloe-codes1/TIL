# Initialization Order of Member Variables

<br>

### Member Variable Initialization Order

> static variable declaration -> field variable declaration -> constructor block
>

- `static variable declaration`
  - Loaded into the `Method area`
  - Variables are initialized first when the class is loaded
- `field variable declaration`
  - Loaded into the `Heap area`
  - Initialized before the constructor block when the object is created
- `constructor block`
  - Loaded into the `Heap area`
  - When the object is created, the JVM internally locks; the visibility of final variables among field variables is initialized after the constructor block ends
  - If already initialized in the field variable declaration, those values are overwritten

<br>

### Initialization Timing

- **`Class variables`**
  - Initialized only once when the class is first loaded
- **`Instance variables`**
  - Initialized for each instance whenever an instance is created

<br>

### Initialization Order

- **`Class variables`**
  - Default value -> Explicit initialization -> Class initialization block
- **`Instance variables`**
  - Default value -> Explicit initialization -> Instance initialization block -> Constructor
