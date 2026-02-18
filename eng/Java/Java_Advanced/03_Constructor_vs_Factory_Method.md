# Constructor vs Factory method

### When to Use a Constructor Instead of a Factory

- The creation logic is not complex
- Object creation is not related to the creation of other objects, and all properties should be passed through the constructor
- The client is interested in the implementation and wants to choose which Strategy pattern to use
- The class is the type itself
  - There is no related hierarchy, so there is no need to choose from a list of concrete implementations
