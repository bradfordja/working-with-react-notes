# Common React Class lifecycle methods

## React class components come with a variety of lifecycle methods that allow developers to tap into different phases of a component's life in the DOM. Here's an overview:

### 1. **`constructor(props)`**

This method is called when a component is being created and before it's mounted.

**Use Case**: Initialize state or bind methods.

**Code Snippet**:
```javascript
constructor(props) {
  super(props);
  this.state = { count: 0 };
  this.handleIncrement = this.handleIncrement.bind(this);
}
```

### 2. **`static getDerivedStateFromProps(props, state)`**

This static method is invoked right before calling `render`.

**Use Case**: Update state based on props changes.

**Code Snippet**:
```javascript
static getDerivedStateFromProps(props, state) {
  if (props.count !== state.prevCountProp) {
    return {
      prevCountProp: props.count,
      count: props.count
    };
  }
  return null;
}
```

### 3. **`shouldComponentUpdate(nextProps, nextState)`**

Decides if the component should be re-rendered.

**Use Case**: Optimize rendering by preventing unnecessary updates.

**Code Snippet**:
```javascript
shouldComponentUpdate(nextProps, nextState) {
  if (this.props.value !== nextProps.value) {
    return true;
  }
  return false;
}
```

### 4. **`render()`**

This method returns the component's output.

**Use Case**: Define your component's UI.

**Code Snippet**:
```javascript
render() {
  return <h1>Hello, {this.props.name}!</h1>;
}
```

### 5. **`componentDidMount()`**

Invoked immediately after the component is added to the DOM.

**Use Case**: Initiate API calls or set up subscriptions.

**Code Snippet**:
```javascript
componentDidMount() {
  fetch('/api/data').then(data => this.setState({ data }));
}
```

### 6. **`componentDidUpdate(prevProps, prevState, snapshot)`**

Invoked after the component gets updated in the DOM.

**Use Case**: Respond to prop or state changes.

**Code Snippet**:
```javascript
componentDidUpdate(prevProps) {
  if (this.props.userID !== prevProps.userID) {
    this.fetchData(this.props.userID);
  }
}
```

### 7. **`componentWillUnmount()`**

Invoked before the component is removed from the DOM.

**Use Case**: Clean up subscriptions or cancel network requests.

**Code Snippet**:
```javascript
componentWillUnmount() {
  clearInterval(this.intervalID);
}
```

Note: There are deprecated lifecycle methods like `componentWillReceiveProps`, `componentWillUpdate`, and `componentWillMount`. They have been superseded by newer methods or strategies and aren't recommended for use in new code. 

## By understanding and leveraging these lifecycle methods, developers can harness the full power of React class components, executing code at precise moments in a component's life in the DOM.