# Core React Concepts

# Question 1.  Explain the concept of Virtual DOM and how React uses it.
### **A. What is the DOM?**
* The **DOM (Document Object Model)** is a tree-like structure that represents your HTML elements in the browser.
* Example:
```html
<div>
  <h1>Hello</h1>
  <p>World</p>
</div>
```
This is represented as a **DOM tree** in the browser.
* The DOM is powerful but **slow to update**, especially when you make frequent changes, because each update triggers layout recalculations, styling, and re-rendering.

### **B. What is the Virtual DOM?**

* The **Virtual DOM (VDOM)** is a **lightweight, in-memory copy of the actual DOM**.
* It’s just a **JavaScript object** that mirrors the real DOM structure.
* Instead of updating the real DOM directly, React updates this Virtual DOM first.

### **C. How React Uses the Virtual DOM**
Here’s the flow:

I. **Initial Render:**
   * React builds a Virtual DOM tree based on your components.
   * It then creates the real DOM from this Virtual DOM.

II. **On State/Props Change:**
   * React **rebuilds a new Virtual DOM** for the updated UI.
   * It then compares the new Virtual DOM with the previous one (this process is called **diffing**).

III. **Reconciliation (Efficient Updates):**
   * React finds only the parts of the DOM that changed.
   * It updates **only those nodes** in the real DOM, instead of re-rendering the entire page.

### **D. Benefits of Virtual DOM**
* **Performance:** Minimizes costly direct manipulations of the real DOM.
* **Efficiency:** Uses **diffing + reconciliation** to batch and optimize updates.
* **Declarative UI:** You just declare *what* the UI should look like, and React figures out *how* to update it efficiently.

✅ **In short:**
The Virtual DOM is a **JavaScript representation of the real DOM** that React uses to make UI updates efficient. React updates the Virtual DOM first, compares it with the old one, and then updates only the necessary parts of the real DOM.

# Question 2.   What are React Fragments?  
A Fragment is a wrapper component in React (<React.Fragment> or shorthand <> </>) that lets you group multiple elements without adding extra nodes to the DOM.  
React Fragments let you group multiple elements without adding an extra node to the DOM. Unlike a div, they don’t create unnecessary wrappers, keeping the DOM clean and avoiding layout/CSS issues. Use <div> only when you need styling or attributes.  

```
<>
  <h1>Title</h1>
  <p>Description</p>
</>
```

# Question 3. What are React Portals?
React Portals let you render children into a DOM node outside the parent hierarchy, useful for modals, tooltips, and dropdowns, while still preserving React’s component structure. 

### **What are React Portals?**
A **Portal** lets you render a React component’s children **into a different place in the DOM tree** than its parent component.
You create one with:
```jsx
ReactDOM.createPortal(child, container)
```
* `child`: JSX you want to render.
* `container`: The DOM node where it should be inserted.

### **When would you use them?**

* When you need a component **visually outside its parent hierarchy** but still want it to behave as part of the React component tree.
* Common use cases:
  1. **Modals / Dialogs**
  2. **Tooltips**
  3. **Dropdowns / Popovers**
  4. **Floating UI elements**

### **Example:**

```jsx
// index.html
<body>
  <div id="root"></div>
  <div id="modal-root"></div>
</body>
```

```jsx
// Modal.js
import ReactDOM from "react-dom";

function Modal({ children }) {
  return ReactDOM.createPortal(
    <div className="modal">{children}</div>,
    document.getElementById("modal-root")
  );
}
```

```jsx
<Modal>
  <h2>This is a modal</h2>
</Modal>
```
👉 Even if you call `<Modal>` inside your app, it renders inside `#modal-root` in the DOM.  

# Question 4. Explain the difference between props and state.

### **1. Props**

* **Definition:** Short for *properties*, props are used to pass **data from parent to child components**.
* **Characteristics:**

  * **Immutable** (read-only inside the child).
  * Passed down from parent → child.
  * Makes components **reusable**.

**Example:**

```jsx
function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}

<Greeting name="Mousharraf" />
```

### **2. State**

* **Definition:** State is **local data storage** managed *within a component*.
* **Characteristics:**

  * **Mutable** (can change over time).
  * Managed internally by the component with `useState` (or `this.state` in class components).
  * When state changes → component re-renders.

**Example:**

```jsx
function Counter() {
  const [count, setCount] = React.useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

### **3. Key Differences**

| Aspect                 | **Props**                            | **State**                         |
| ---------------------- | ------------------------------------ | --------------------------------- |
| **Who owns it?**       | Parent (passed down)                 | Component itself                  |
| **Mutable?**           | ❌ Immutable                          | ✅ Mutable                         |
| **Usage**              | Pass data/config to child components | Store data that changes over time |
| **Trigger Re-render?** | No (unless parent re-renders)        | Yes, when state changes           |

---

✅ **In short (interview-ready):**
* **Props** are inputs passed from parent to child, **read-only**.
* **State** is data managed inside a component, **can change**, and causes re-renders.

Do you want me to also give you a **one-liner analogy** (like a real-life example) so it’s easier to recall in an interview?

# Question 5. Props can be used to pass the data from child to praent as well 

* **Props flow parent → child.**
* But if you want the **child to send data back to the parent**, you pass a **callback function as a prop**.  

So the **data still flows down** (the function is passed from parent to child), but the **execution flows up** (child calls the function → parent receives data).

### 🔹 Example

```jsx
// Parent
function Parent() {
  const [message, setMessage] = React.useState("");

  const handleChildMessage = (data) => {
    setMessage(data);
  };

  return (
    <>
      <Child sendMessage={handleChildMessage} />
      <p>Message from child: {message}</p>
    </>
  );
}

// Child
function Child({ sendMessage }) {
  return (
    <button onClick={() => sendMessage("Hello Parent!")}>
      Send Message
    </button>
  );
}
```

👉 Here:
* `sendMessage` (a function) is **passed from parent → child as a prop**.
* The child **invokes** it to pass data back **to the parent**.

### ✅ Interview One-Liner
**Props are always passed from parent to child, but using callback props, a child can “notify” or send data back to the parent.**


