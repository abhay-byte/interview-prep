### **React.js: 20 Theoretical & Conceptual Questions**

**1. Q: What is React, and what are its main features?**
*   **A:** React is a JavaScript library for building user interfaces, primarily for single-page applications. Its main features are:
    *   **Component-Based Architecture:** UI is broken down into reusable, independent pieces called components.
    *   **Virtual DOM:** React uses an in-memory representation of the real DOM to minimize direct DOM manipulation, which is slow. It calculates the minimal changes needed and updates the real DOM efficiently.
    *   **JSX (JavaScript XML):** A syntax extension that allows you to write HTML-like code within JavaScript, making component creation more intuitive.
    *   **One-Way Data Flow:** Data flows in a single direction (from parent to child components), which makes the application state more predictable and easier to debug.

**2. Q: What is the difference between the Virtual DOM and the Real DOM?**
*   **A:**
    *   **Real DOM:** The actual tree-like structure of HTML elements in the browser that represents the UI. Direct manipulation of the Real DOM is slow because it triggers reflows and repaints.
    *   **Virtual DOM (VDOM):** An in-memory, lightweight copy of the Real DOM. When state changes, React creates a new VDOM, compares it with the previous VDOM (a process called "diffing"), and calculates the most efficient batch of updates to apply to the Real DOM. This process is called **reconciliation**.

**3. Q: What is JSX?**
*   **A:** JSX stands for JavaScript XML. It's a syntax extension that lets you write HTML-like structures directly in your JavaScript code. It is not valid JavaScript and must be transpiled by tools like Babel into standard `React.createElement()` calls. It makes component code more readable and declarative.

**4. Q: What is the difference between a Class Component and a Functional Component?**
*   **A:**
    *   **Class Components:** ES6 classes that extend `React.Component`. They manage state using `this.state` and handle lifecycle events with methods like `componentDidMount()`. They are considered the "old" way of writing stateful components.
    *   **Functional Components:** Simple JavaScript functions that accept props and return JSX. With the introduction of **Hooks**, they can now manage state (`useState`), handle side effects (`useEffect`), and access other React features, making them the modern standard for writing components.

**5. Q: What are props, and how are they different from state?**
*   **A:**
    *   **Props (Properties):** Read-only data passed from a parent component to a child component. They are immutable within the child component. Think of them as function arguments.
    *   **State:** Data that is managed *within* a component. It is mutable and can be changed by the component itself (using `this.setState` or `useState`). When state changes, React re-renders the component.

**6. Q: What are Hooks in React?**
*   **A:** Hooks are functions (like `useState`, `useEffect`) that let you "hook into" React state and lifecycle features from functional components. They were introduced to allow for stateful logic in functional components without converting them into classes.

**7. Q: Explain the `useState` Hook.**
*   **A:** `useState` is a Hook that adds state to a functional component. It returns an array with two elements: the current state value and a function to update that value. Calling the update function will trigger a re-render of the component with the new state value.

**8. Q: Explain the `useEffect` Hook and its dependency array.**
*   **A:** `useEffect` is a Hook for handling **side effects** in functional components, such as data fetching, subscriptions, or manually changing the DOM. The dependency array controls when the effect runs:
    *   **No array:** The effect runs after *every* render.
    *   **Empty array `[]`:** The effect runs only *once*, after the initial render (similar to `componentDidMount`).
    *   **Array with values `[prop, state]`:** The effect runs only when any of the values in the array change.

**9. Q: What is "prop drilling" and how can you solve it?**
*   **A:** **Prop drilling** is the process of passing props down through multiple layers of nested components to reach a deeply nested child that needs the data. This can become cumbersome. It is solved using:
    *   **Context API:** A built-in React feature that allows you to share state across the entire component tree without passing props down manually.
    *   **State Management Libraries:** Tools like Redux or Zustand centralize application state in a global "store."

**10. Q: What is the purpose of "keys" when rendering lists?**
*   **A:** Keys are a special string attribute you need to include when creating lists of elements. React uses these keys to identify which items have changed, been added, or been removed. They help React efficiently update the UI by giving each element a stable identity across re-renders. Using the array index as a key is an anti-pattern if the list can be reordered or filtered.

**11. Q: What is conditional rendering?**
*   **A:** Conditional rendering is the practice of rendering different JSX markup based on certain conditions (e.g., a state variable). This can be achieved using standard JavaScript operators like `if/else` statements, the ternary operator (`condition ? <JSX1> : <JSX2>`), or logical operators like `&&`.

**12. Q: What are Controlled and Uncontrolled Components?**
*   **A:** This distinction primarily applies to form elements:
    *   **Controlled Component:** An input form element whose value is controlled by React state. The state is the "single source of truth," and its value is updated via an `onChange` handler.
    *   **Uncontrolled Component:** A form element where the DOM handles the state internally. You typically use a `ref` to get its value when needed (e.g., on form submission).

**13. Q: What is "lifting state up"?**
*   **A:** "Lifting state up" is a common pattern in React where you move the shared state from multiple child components up to their closest common ancestor. The ancestor then passes the state and update functions down to the children as props, ensuring a single source of truth.

**14. Q: What are Higher-Order Components (HOCs)?**
*   **A:** A Higher-Order Component is an advanced React pattern for reusing component logic. A HOC is a function that takes a component as an argument and returns a new component, usually with additional props or behavior.

**15. Q: What are `useMemo` and `useCallback` used for?**
*   **A:** Both are Hooks used for performance optimization by memoizing (caching) values to prevent unnecessary re-computations.
    *   `useMemo`: Memoizes the **return value** of a function. It re-runs the function only if one of its dependencies has changed. Use it for expensive calculations.
    *   `useCallback`: Memoizes the **function definition** itself. It returns the same function instance between renders unless a dependency changes. Use it to prevent child components from re-rendering unnecessarily when passed a function as a prop.

**16. Q: What is the Context API?**
*   **A:** The Context API provides a way to pass data through the component tree without having to pass props down manually at every level. You create a `Context`, provide a value to it at a high level, and any component within that tree can consume the value.

**17. Q: What is a React Fragment?**
*   **A:** A React Fragment (`<></>`) is a feature that lets you group a list of children without adding extra nodes to the DOM. This is useful because a component's `render` method must return a single root element.

**18. Q: Why should you not modify state directly?**
*   **A:** You should never modify state directly (e.g., `this.state.count = 1` or `myState.key = 'value'`). You must use the state updater function (`this.setState()` or `setMyState()`). Modifying state directly will not trigger a re-render, leading to an inconsistent UI.

**19. Q: What is the component lifecycle in React?**
*   **A:** The component lifecycle is a sequence of phases a component goes through from its creation to its destruction. The main phases are:
    *   **Mounting:** The component is being created and inserted into the DOM (`componentDidMount`, `useEffect` with `[]`).
    *   **Updating:** The component is re-rendering due to changes in its props or state (`componentDidUpdate`, `useEffect` with dependencies).
    *   **Unmounting:** The component is being removed from the DOM (`componentWillUnmount`, the cleanup function in `useEffect`).

**20. Q: What is a custom hook?**
*   **A:** A custom hook is a reusable JavaScript function whose name starts with "use" and that can call other hooks. It's a way to extract and share stateful logic between different functional components without using HOCs or render props.