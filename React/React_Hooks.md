# React Hooks

> References: [velopert](https://velog.io/@velopert/react-hooks)

<br>

<br>

## 1. useState

- 가장 기본적인 `Hook` 으로서, **functional component** 에서도 가변적인 상태를  지니고 있을 수 있게 해줌
- 함수형 component에서 상태를 관리해야 될 때, `Hook`을 사용하면 된다!

<br>

<br>

## 2. useEffect

- React component가 rendering 될 때마다 특정 작업을 수행하도록 설정할 수 있는 `Hook`
- **class component** 의 `componentDidMount` 와 `componentDidUpdate` 를 합친 것이라고 보면 됨!
- rendering 되고 난 직후마다 실행 됨
- 두 번째 parameter 배열에 무엇을 넣느냐에 따라 실행되는 조건이 달라짐

<br>

### 2-1. `useEffect`를 component가 mount 될 때만 실행하고 싶을 때

- 화면에 처음 rendering 될 때만 실행하고, update 될 때 실행할 필요 없을 때,

  - 두 번째 parameter로 비어있는 배열 ( `[]` )  를 넣어주면 됨

    ex)

    ```react
    useEffect( ()=> {
        console.log('이렇게 하면 mount 될 때만 실행!')
    }, [])
    ```

<br>

### 2-2. 특정 값이 update 될 때만 실행하고 싶을 때

ex)

```react
useEffect( () => {
    console.log('새해에 나이 바뀔 때 실행될거얌')
}, [age])
```

<br>

<br>
