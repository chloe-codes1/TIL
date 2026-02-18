# React Hooks

> References: [velopert](https://velog.io/@velopert/react-hooks)

<br>

<br>

## 1. useState

- The most basic `Hook` that allows **functional components** to hold mutable state
- When you need to manage state in a functional component, use `Hooks`!

<br>

<br>

## 2. useEffect

- A `Hook` that allows you to set up specific tasks to be performed each time a React component renders
- Think of it as a combination of `componentDidMount` and `componentDidUpdate` from **class components**!
- Executed right after each render
- The execution conditions differ depending on what you put in the second parameter array

<br>

### 2-1. When you want `useEffect` to run only when the component mounts

- When you want it to run only on the first render, and not when updated,

  - Pass an empty array ( `[]` ) as the second parameter

    ex)

    ```react
    useEffect( ()=> {
        console.log('This runs only when mounted!')
    }, [])
    ```

<br>

### 2-2. When you want to run only when a specific value updates

ex)

```react
useEffect( () => {
    console.log('This will run when age changes on New Year!')
}, [age])
```

<br>

<br>
