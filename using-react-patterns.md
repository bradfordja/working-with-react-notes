# Using React patterns development 

## Below is a list of common React patterns with simple explanations, sample use-cases:

### 1. Function Components

**Explanation**: This is the simplest way to define a React component using a JavaScript function.

**Use-Case**: Displaying a simple greeting message.

```jsx
// Function component for displaying a greeti6ng
function Greeting({ name }) {
  return <p>Hello, {name}!</p>;
}
```

### 2. Class Components

**Explanation**: Defines a React component using an ES6 class.

**Use-Case**: When you need local state or lifecycle methods.

```jsx
// Class component
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  // Method to increment count
  increment = () => {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return (
      <button onClick={this.increment}>
        Count: {this.state.count}
      </button>
    );
  }
}
```

### 3. Container and Presentation Components

**Explanation**: Separating business logic from presentation.

**Use-Case**: Fetching and displaying a list of items.

```jsx
// Container component
function ItemListContainer() {
  const items = fetchData();
  return <ItemList items={items} />;
}

// Presentation component
function ItemList({ items }) {
  return (
    <ul>
      {items.map(item => <li key={item.id}>{item.name}</li>)}
    </ul>
  );
}
```

### 4. Controlled Components

**Explanation**: Components where React manages the form inputs.

**Use-Case**: A form with validation.

```jsx
// Controlled component
function ControlledForm() {
  const [email, setEmail] = React.useState('');

  return (
    <input
      type="email"
      value={email}
      onChange={e => setEmail(e.target.value)}
    />
  );
}
```

### 5. Uncontrolled Components

**Explanation**: Components that use DOM to handle form inputs.

**Use-Case**: A simple form with no validation.

```jsx
// Uncontrolled component
function UncontrolledForm() {
  const inputRef = React.useRef();

  const handleSubmit = () => {
    console.log(inputRef.current.value);
  };

  return (
    <input ref={inputRef} type="text" />
  );
}
```

### 6. Higher-Order Components (HOC)

**Explanation**: A function that takes a component and returns a new component.

**Use-Case**: Code reuse, for instance, loading data from an API.

```jsx
// Higher-Order Component
function withData(WrappedComponent) {
  return function WithData(props) {
    const data = fetchData();
    return <WrappedComponent data={data} {...props} />;
  };
}
```

### 7. Render Props

**Explanation**: A pattern where a component takes a function prop and that function returns JSX.

**Use-Case**: Sharing behavior between components, such as mouse tracking.

```jsx
// Using render prop
function MouseTracker({ render }) {
  const [position, setPosition] = React.useState({ x: 0, y: 0 });

  return (
    <div onMouseMove={e => setPosition({ x: e.clientX, y: e.clientY })}>
      {render(position)}
    </div>
  );
}
```

### 8. Compound Components

**Explanation**: Components that work together, sharing an implicit state.

**Use-Case**: Building complex UI components like a `Tabs` component.

```jsx
// Compound Components
function Tabs({ children }) {
  const [activeIndex, setActiveIndex] = React.useState(0);
  return (
    <>
      {React.Children.map(children, (child, index) =>
        React.cloneElement(child, { active: index === activeIndex, setActiveIndex })
      )}
    </>
  );
}
```

### 9. Context API

**Explanation**: Provides a way to share data between components without passing props.

**Use-Case**: Storing and retrieving user authentication status.

```jsx
// Context API
const AuthContext = React.createContext();

function AuthProvider({ children }) {
  const [isLoggedIn, setIsLoggedIn] = React.useState(false);
  return (
    <AuthContext.Provider value={{ isLoggedIn, setIsLoggedIn }}>
      {children}
    </AuthContext.Provider>
  );
}
```

### 10. Hooks

**Explanation**: Functions that let you use state and lifecycle features in functional components.

**Use-Case**: Using state in functional components.

```jsx
// Using Hooks
function Counter() {
  const [count, setCount] = React.useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

### 11. Custom Hooks

**Explanation**: Extracting hook logic into reusable functions.

**Use-Case**: Sharing data fetching logic across components.

```jsx
// Custom Hook for data fetching
function useFetch(url) {
  const [data, setData] = React.useState(null);

  React.useEffect(() => {
    fetch(url).then(response => response.json()).then(setData);
  }, [url]);

  return data;
}
```

### 12. Prop Drilling

**Explanation**: Passing props from a parent component down to a nested child component.

**Use-Case**: Sharing state between distant relatives in the component tree.

```jsx
// Prop drilling
function Parent() {
  const [state, setState] = React.useState('some state');

  return <Child1 state={state} />;
}

function Child1({ state }) {
  return <Child2 state={state} />;
}

function Child2({ state }) {
  return <div>{state}</div>;
}
```

### 13. Lazy Loading

**Explanation**: Loading components as they're needed rather than all at once.

**Use-Case**: Performance optimization for larger applications.

```jsx
// Lazy loading a component
const LazyComponent = React.lazy(() => import('./LazyComponent'));

function App() {
  return (
    <React.Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </React.Suspense>
  );
}
```

### 14. Conditional Rendering

**Explanation**: Render different UI elements based on some condition.

**Use-Case**: Show/hide elements based on user authentication.

```jsx
// Conditional rendering
function Greeting({ isLoggedIn }) {
  return isLoggedIn ? <div>Welcome, user!</div> : <div>Please log in.</div>;
}
```

### 15. Fragments

**Explanation**: A way to return multiple elements without wrapping them in a div.

**Use-Case**: Returning multiple table rows.

```jsx
// Using Fragments
function Table() {
  return (
    <React.Fragment>
      <tr><td>Row1</td></tr>
      <tr><td>Row2</td></tr>
    </React.Fragment>
  );
}
```

### 16. Memoization

**Explanation**: Optimizing component re-rendering.

**Use-Case**: Avoiding re-renders of expensive components.

```jsx
// Using React.memo for functional component
const ExpensiveComponent = React.memo(function Expensive({ prop }) {
  // Expensive calculations
  return <div>{prop}</div>;
});
```

### 17. Portals

**Explanation**: Rendering children into a DOM node that exists outside the DOM hierarchy of the parent component.

**Use-Case**: Modals or tooltips.

```jsx
// Using Portals
function Modal({ children }) {
  return ReactDOM.createPortal(
    children,
    document.getElementById('modal-root')
  );
}
```

### 18. Error Boundaries

**Explanation**: Catch and handle JavaScript errors in child component trees.

**Use-Case**: Gracefully degrade the UI in case of errors.

```jsx
// Error Boundary
class ErrorBoundary extends React.Component {
  // ...lifecycle methods to handle errors
}
```

### 19. Forward Refs

**Explanation**: Passing down `ref` through components.

**Use-Case**: Accessing a DOM element in a child component.

```jsx
// Forwarding refs
const ForwardingComponent = React.forwardRef((props, ref) => (
  <button ref={ref}>Click Me!</button>
));
```

### 20. Provider Pattern

**Explanation**: Using a component to provide some context or state to its descendants.

**Use-Case**: Theme provider, Localization provider.

```jsx
// ThemeProvider Component
export const ThemeContext = React.createContext();

export function ThemeProvider({ children }) {
  return (
    <ThemeContext.Provider value="dark">
      {children}
    </ThemeContext.Provider>
  );
}
```

### 21. Global State with Context and Reducer

**Explanation**: Managing global state using `useContext` and `useReducer`.

**Use-Case**: Shared authentication state.

```jsx
const AuthContext = React.createContext();

function AuthProvider({ children }) {
  const [state, dispatch] = React.useReducer(authReducer, initialState);
  return (
    <AuthContext.Provider value={{ state, dispatch }}>
      {children}
    </AuthContext.Provider>
  );
}

function authReducer(state, action) {
  // logic here
}
```

### 22. Imperative Handles

**Explanation**: Expose imperative methods of a component using `useImperativeHandle`.

**Use-Case**: Manual focus on an input.

```jsx
const TextInput = React.forwardRef((props, ref) => {
  const inputRef = React.useRef();

  React.useImperativeHandle(ref, () => ({
    focus: () => inputRef.current.focus()
  }));

  return <input ref={inputRef} />;
});
```

### 23. Debouncing

**Explanation**: Delay the execution of functions.

**Use-Case**: Real-time search.

```jsx
function Search() {
  const [query, setQuery] = React.useState('');

  const debouncedQuery = useDebounce(query, 300);

  React.useEffect(() => {
    if (debouncedQuery) {
      fetchResults(debouncedQuery);
    }
  }, [debouncedQuery]);

  return (
    <input onChange={e => setQuery(e.target.value)} />
  );
}
```

### 24. Throttling Events

**Explanation**: Limit the rate a function can execute.

**Use-Case**: Infinite scrolling.

```jsx
// Use a custom hook or library to throttle scroll events
```

### 25. Reusable Styles

**Explanation**: Reusing styles using CSS-in-JS libraries or utility-first CSS.

**Use-Case**: Reusable button with different variants.

```jsx
// Reusable button with styled-components or Tailwind
```

### 26. Server-Side Rendering (SSR)

**Explanation**: Rendering React components on the server for better performance and SEO.

**Use-Case**: SEO-heavy or performance-sensitive applications.

```jsx
// This is generally achieved through frameworks like Next.js
```

### 27. Static Site Generation (SSG)

**Explanation**: Generating static HTML files at build time.

**Use-Case**: Blogs, documentation sites.

```jsx
// Use Next.js or Gatsby for SSG
```

### 28. Dynamic Imports

**Explanation**: Lazily load modules.

**Use-Case**: Splitting code for better performance.

```jsx
// Lazy load a module
const OtherComponent = React.lazy(() => import('./OtherComponent'));
```

### 29. Suspense for Data Fetching

**Explanation**: Lets components “wait” for something before rendering.

**Use-Case**: Fetching data from an API.

```jsx
// This feature is experimental but you would use <React.Suspense>
```

### 30. Batched Updates

**Explanation**: Batch multiple `setState` calls into a single update.

**Use-Case**: Minimizing re-renders.

```jsx
// Achieved automatically in event handlers, or manually using ReactDOM.unstable_batchedUpdates()
```

Please note that for some patterns like SSR, SSG, or Suspense for data fetching, the explanation may involve the use of specific frameworks or experimental features, and they can't be easily demonstrated through a simple code snippet.

### 31. Memoization with useMemo

**Explanation**: Optimize expensive calculations by memoizing the result.

**Use-Case**: Avoid redundant calculations.

```jsx
function Fibonacci({ n }) {
  const fib = useMemo(() => calculateFibonacci(n), [n]);
  return <div>{`Fibonacci(${n}) = ${fib}`}</div>;
}
```

### 32. Error Boundaries

**Explanation**: Catch and handle errors in component trees.

**Use-Case**: Graceful degradation of UI.

```jsx
class ErrorBoundary extends React.Component {
  componentDidCatch(error, info) {
    // Handle error
  }
  render() {
    return this.props.children;
  }
}
```

### 33. Forwarding Refs

**Explanation**: Pass `ref` through a component to one of its children.

**Use-Case**: Control child component instances or DOM elements.

```jsx
const ForwardedInput = React.forwardRef((props, ref) => (
  <input ref={ref} {...props} />
));
```

### 34. Reusable Logic with Custom Hooks

**Explanation**: Extract component logic into reusable functions.

**Use-Case**: Share logic across multiple components.

```jsx
function useCounter() {
  const [count, setCount] = useState(0);
  const increment = () => setCount(count + 1);
  return { count, increment };
}
```

### 35. Optimistic UI Updates

**Explanation**: Assume a successful operation and update the UI, reverting back in case of error.

**Use-Case**: Immediate UI feedback for better user experience.

```jsx
function deleteItem(id) {
  // Optimistically remove item from UI
  removeItemFromState(id);

  api.delete(`/items/${id}`).catch(() => {
    // Revert UI changes if deletion fails
  });
}
```

### 36. State Machines

**Explanation**: Formal representation of a component's behavior and state transitions.

**Use-Case**: Complex forms, workflows.

```jsx
// Use a state machine library like XState
```

### 37. Testing Patterns

**Explanation**: Patterns to make your React components more testable.

**Use-Case**: Unit testing, integration testing.

```jsx
// Use libraries like Jest and the React Testing Library
```

### 38. Dependency Injection

**Explanation**: Inject dependencies into components for better modularity and testability.

**Use-Case**: Making components more decoupled and easier to test.

```jsx
function Greeting({ userService }) {
  const username = userService.getUsername();
  return <p>Hello, {username}</p>;
}
```

### 39. Proxy Components

**Explanation**: Enhance components by wrapping them.

**Use-Case**: Add props or alter behavior of children components.

```jsx
function EnhancedButton({ children }) {
  return React.cloneElement(children, { disabled: true });
}
```

### 40. Skeleton Loading

**Explanation**: Display a skeleton of the UI while data is being fetched.

**Use-Case**: Improve perceived performance.

```jsx
function UserComponent({ data }) {
  return data ? <div>{data.name}</div> : <div className="skeleton"></div>;
}
```

### 41. Recoil for State Management

**Explanation**: An experimental state management library from Facebook.

**Use-Case**: When you need more complex state relations that Context can't efficiently handle.

```jsx
import { atom, useRecoilState } from 'recoil';

const countState = atom({
  key: 'countState',
  default: 0,
});

function Counter() {
  const [count, setCount] = useRecoilState(countState);
  return <button onClick={() => setCount(count + 1)}>Count: {count}</button>;
}
```

### 42. SWR for Data Fetching

**Explanation**: A library for data fetching with built-in caching.

**Use-Case**: Fetching and revalidating data on the client side.

```jsx
import useSWR from 'swr';

function Profile() {
  const { data, error } = useSWR('/api/user', fetch);

  if (error) return <div>Error</div>;
  if (!data) return <div>Loading...</div>;

  return <div>Hello {data.name}</div>;
}
```

### 43. Atomic Design

**Explanation**: A methodology for creating design systems.

**Use-Case**: Building UI in a scalable and maintainable way.

```jsx
// Organize components into atoms, molecules, organisms, templates, and pages
```

### 44. CQRS (Command Query Responsibility Segregation)

**Explanation**: Separates read and write operations.

**Use-Case**: Large scale applications with complex business logic.

```jsx
// Typically used on the backend but can also affect frontend architecture
```

### 45. Event Sourcing

**Explanation**: Store state as a sequence of events.

**Use-Case**: Applications where state needs to be reconstructed.

```jsx
// Primarily a backend pattern but can influence how frontend sends updates
```

## Note: Some patterns like CQRS and Event Sourcing are generally more prevalent in backend development but can have implications on how you design your React components and manage state. Similarly, methodologies like Atomic Design are more overarching and affect your entire project structure rather than individual components.