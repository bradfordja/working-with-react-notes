# Common React Functional lifecycle hooks

## React hooks are essential for managing stateful logic and side effects in functional components. 

### 1. useState:
useState is used to add state to functional components. It returns a state variable and a function to update that variable.

Code Snippet:
```jsx
import React, { useState } from 'react';

function ExampleComponent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

### 2. useEffect:
useEffect is used to perform side effects in functional components, such as data fetching, subscriptions, or DOM manipulation.

Code Snippet:
```jsx
import React, { useEffect, useState } from 'react';

function ExampleComponent() {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetchData();
  }, []);

  const fetchData = async () => {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    setData(data);
  };

  return (
    <div>
      {data.map((item) => (
        <p key={item.id}>{item.name}</p>
      ))}
    </div>
  );
}
```

### 3. useContext:
useContext is used to access the value of a React context in functional components.

Code Snippet:
```jsx
import React, { useContext } from 'react';

const MyContext = React.createContext();

function ExampleComponent() {
  const contextValue = useContext(MyContext);

  return <p>Value from Context: {contextValue}</p>;
}
```

### 4. useReducer:
useReducer is an alternative to useState for managing complex state logic, especially when the state transitions are more advanced.

Code Snippet:
```jsx
import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function ExampleComponent() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
    </div>
  );
}
```

### 5. useCallback:
Explanation: useCallback is used to memoize a function so that it does not change between renders, preventing unnecessary re-renders of child components.

Code Snippet:
```jsx
import React, { useCallback, useState } from 'react';

function ExampleComponent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    setCount(count + 1);
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
}
```

### 6. useMemo:
Explanation: useMemo is used to memoize the result of a computation so that it is not recalculated on every render, improving performance.

Code Snippet:
```jsx
import React, { useMemo } from 'react';

function ExampleComponent({ data }) {
  const expensiveComputation = useMemo(() => {
    // Expensive computation based on data
    return data.reduce((acc, item) => acc + item, 0);
  }, [data]);

  return <p>Result: {expensiveComputation}</p>;
}
```

### 7. useRef:
Explanation: useRef is used to hold a mutable value that does not trigger re-renders when it changes.

Code Snippet:
```jsx
import React, { useRef } from 'react';

function ExampleComponent() {
  const inputRef = useRef();

  const handleFocus = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
}
```

### 8. useLayoutEffect:
Explanation: useLayoutEffect is similar to useEffect but fires synchronously after all DOM mutations. It's rarely needed but can be useful in certain situations.

Code Snippet:
```jsx
import React, { useLayoutEffect, useState } from 'react';

function ExampleComponent() {
  const [width, setWidth] = useState(0);

  useLayoutEffect(() => {
    const handleResize = () => {
      setWidth(window.innerWidth);
    };
    window.addEventListener('resize', handleResize);
    handleResize();
    return () => {
      window.removeEventListener('resize', handleResize);
    };
  }, []);

  return <p>Window Width: {width}</p>;
}
```

### 9. useImperativeHandle:
Explanation: useImperativeHandle customizes the instance value that is exposed to parent components when using ref.

Code Snippet:
```jsx
import React, { useRef, useImperativeHandle } from 'react';

const ChildComponent = React.forwardRef((props, ref) => {
  const inputRef = useRef();

  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    },
  }));

  return <input ref={inputRef} type="text" />;
});

function ParentComponent() {
  const childRef = useRef();

  const handleFocus = () => {
    childRef.current.focus();
  };

  return (
    <div>
      <ChildComponent ref={childRef} />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
}
```

### 10. useDebugValue:
Explanation: useDebugValue is used to display custom labels for custom hooks in React DevTools.

Code Snippet:
```jsx
import { useDebugValue, useState } from 'react';

function useCustomHook(initialState) {
  const [value, setValue] = useState(initialState);
  useDebugValue(`Custom Hook Value: ${value}`);
  return [value, setValue];
}

function ExampleComponent() {
  const [count, setCount] = useCustomHook(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

## These 10 React hooks are commonly used in modern React applications. Familiarity with these hooks will allow you to efficiently manage stateful logic and side effects in functional components. Good luck with the interview!