# 100 Conceptual and Basic Questions on MERN Stack

---

### **1. What are micro and macro queues in JavaScript?**

**Explanation:**

JavaScript uses an **event loop** to handle asynchronous operations. This event loop manages two main types of queues:

- **Microtask Queue:**

  - **What It Is:** This queue handles tasks that need to be executed immediately after the current script finishes but before any other tasks (macrotasks) are processed.
  - **Examples:** Promises (`.then()`, `.catch()`), `MutationObserver`.
  - **Execution:** Microtasks are processed right after the current task and before any macrotasks or rendering updates.

- **Macrotask Queue:**
  - **What It Is:** This queue handles tasks that are executed after the current script and all microtasks have been processed.
  - **Examples:** `setTimeout()`, `setInterval()`, I/O operations (like reading a file).
  - **Execution:** Macrotasks are processed one by one in the order they are scheduled.

**How It Works:**

1. JavaScript runs the current script, including synchronous code.
2. Once the script finishes, the event loop processes all microtasks.
3. After all microtasks are done, the event loop processes one macrotask.
4. If there are any changes that need to be rendered (like updating the UI), those are handled next.

**Example:**

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Macrotask: setTimeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Microtask: Promise");
});

console.log("End");
```

**Output:**

```
Start
End
Microtask: Promise
Macrotask: setTimeout
```

**Explanation:**

- The synchronous logs `Start` and `End` run first.
- The `Promise` (microtask) is executed next because microtasks run before macrotasks.
- The `setTimeout` (macrotask) runs last.

---

### **2. What are promises in JavaScript?**

**Explanation:**

A **Promise** is a special object in JavaScript used for handling asynchronous operations. It represents a value that may be available now, later, or never.

- **States of a Promise:**

  - **Pending:** The promise is still waiting for the result.
  - **Fulfilled:** The operation completed successfully, and the promise has a result.
  - **Rejected:** The operation failed, and the promise has an error.

- **Methods to Work with Promises:**
  - **`.then(onFulfilled, onRejected)`**: Use this to specify what should happen when the promise is fulfilled or rejected.
  - **`.catch(onRejected)`**: Use this to handle errors.
  - **`.finally(onFinally)`**: Use this to run code after the promise is settled, regardless of the outcome.

**How It Works:**

1. When you create a promise, you provide a function with `resolve` and `reject` arguments.
2. Call `resolve` if the operation is successful or `reject` if it fails.
3. Use `.then()` to handle successful results, `.catch()` to handle errors, and `.finally()` for cleanup.

**Example:**

```javascript
let promise = new Promise((resolve, reject) => {
  let success = true; // Simulate a success scenario
  if (success) {
    resolve("Operation was successful!");
  } else {
    reject("Operation failed.");
  }
});

promise
  .then((result) => console.log(result)) // Handles success
  .catch((error) => console.error(error)) // Handles failure
  .finally(() => console.log("Operation finished."));
```

**Explanation:**

- **Promise Creation:** `resolve` or `reject` is called based on whether the operation was successful.
- **Handling Results:** Use `.then()` for success, `.catch()` for errors, and `.finally()` for any code that needs to run after the promise is settled.

---

### **3. How do asynchronous functions work?**

**Explanation:**

**Asynchronous functions** are a modern way to handle asynchronous operations in JavaScript. They use the `async` keyword and allow you to use the `await` keyword to pause execution until a promise is settled.

- **`async` Function:**

  - **Definition:** Declares a function that returns a promise. Inside this function, you can use `await` to wait for other promises.
  - **Behavior:** Automatically wraps return values in a promise.

- **`await` Keyword:**
  - **Definition:** Pauses the execution of the `async` function until the promise resolves.
  - **Usage:** Can only be used inside `async` functions.

**How It Works:**

1. Define a function with `async` keyword.
2. Inside this function, use `await` to pause until a promise resolves.
3. Continue with the code after the `await` statement.

**Example:**

```javascript
async function fetchData() {
  let result = await new Promise((resolve) =>
    setTimeout(() => resolve("Data fetched"), 1000)
  );
  console.log(result);
}

fetchData();
console.log("Fetching data...");
```

**Explanation:**

- **`fetchData()`** is an `async` function that waits for the promise to resolve before logging the result.
- **`console.log('Fetching data...')`** executes immediately while waiting for the promise.

---

### **4. What is the Fetch API?**

**Explanation:**

The **Fetch API** is a modern way to make network requests (like HTTP requests) in JavaScript. It provides a simpler and more powerful alternative to older methods like `XMLHttpRequest`.

- **Basic Usage:**

  - **`fetch(url, options)`**: Starts a network request.
  - Returns a **Promise** that resolves to a **Response** object.

- **Response Object:**
  - **`.json()`**: Parses the response body as JSON.
  - **`.text()`**: Parses the response body as plain text.
  - **`.blob()`**: Returns the response body as a binary object.

**How It Works:**

1. Call `fetch()` with the URL and options (if needed).
2. The returned promise resolves to a `Response` object.
3. Use methods like `.json()` to extract data from the response.

**Example:**

```javascript
fetch("https://jsonplaceholder.typicode.com/posts")
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

**Explanation:**

- **`fetch()`** makes a network request.
- **`.then()`** handles the response and converts it to JSON.
- **`.catch()`** handles any errors that occur during the fetch.

---

### **5. How do arrays and objects work in JavaScript?**

**Explanation:**

In JavaScript, **arrays** and **objects** are fundamental data structures used to store and manage collections of data.

- **Arrays:**

  - **Definition:** An ordered collection of values. Each value (element) is identified by an index, starting from 0.
  - **Creation:** You create an array using square brackets `[]`.

  **Example:**

  ```javascript
  let fruits = ["Apple", "Banana", "Cherry"];
  console.log(fruits[0]); // Output: 'Apple'
  ```

  - **Common Methods:**
    - **`.push(item)`**: Adds an item to the end.
    - **`.pop()`**: Removes the last item.
    - **`.shift()`**: Removes the first item.
    - **`.unshift(item)`**: Adds an item to the beginning.

- **Objects:**

  - **Definition:** An unordered collection of key-value pairs. Each key (property) is a string, and each value can be any data type.
  - **Creation:** You create an object using curly braces `{}`.

  **Example:**

  ```javascript
  let person = {
    name: "John",
    age: 30,
  };
  console.log(person.name); // Output: 'John'
  ```

  - **Common Methods:**
    - **`.hasOwnProperty(key)`**: Checks if an object has a specific property.
    - **`delete object.key`**: Removes a property.

**How They Work:**

- **Arrays** are indexed collections, ideal for ordered data and list operations.
- **Objects** are key-value pairs, suitable for structured data and lookups.

---

### **6. What is the event loop in JavaScript?**

**Explanation:**

The **event loop** is a mechanism that allows JavaScript to handle asynchronous operations like I/O, network requests, and timers without blocking the main thread.

- **How It Works:**

  1. **Call Stack:** This is where JavaScript executes synchronous code. It follows Last In, First Out (LIFO) principle.
  2. **Task Queues:** Includes microtasks (e.g., promises) and macrotasks (e.g., `setTimeout`).
  3. **Event Loop:** Continuously checks if the call stack is empty and then processes tasks from the queues.

- **Process:**
  1. Execute all the synchronous code in the call stack.
  2. Process all microtasks (like promises).
  3. Process one macrotask (like `setTimeout`).
  4. Render updates (if necessary).

**Example:**

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Macrotask: setTimeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Microtask: Promise");
});

console.log("End");
```

**Explanation:**

- **Synchronous Code:** `Start` and `End` are printed first.
- **Microtasks:** `Promise` is printed next.
- **Macrotasks:** `setTimeout` is printed last.

---

### **7. How does the call stack work in JavaScript?**

**Explanation:**

The **call stack** is a data structure used by JavaScript to keep track of function calls and their execution contexts.

- **How It Works:**
  1. **Push:** When a function is called, its context (information about the function) is pushed onto the stack.
  2. **Pop:** When the function completes, its context is popped off the stack.
  3. **Execution Order:** Functions are executed in the order they are called and completed.

**Example:**

```javascript
function first() {
  console.log("First");
  second();
}

function second() {
  console.log("Second");
}

first();
```

**Explanation:**

- **Call Stack Execution:** `first()` is pushed onto the stack, executes, calls `second()`, which is then pushed and executed.
- **Stack Unwinds:** After `second()` completes, it's popped off, followed by `first()`.

---

### **8. What is Cross-Origin Resource Sharing (CORS)?**

**Explanation:**

**CORS** is a security feature that allows or restricts web applications running at one origin to access resources from another origin (domain).

- **What It Does:**

  - **Allows Safe Cross-Origin Requests:** CORS specifies which domains are permitted to access resources on your server.
  - **Preflight Requests:** For certain types of requests (like those with custom headers or methods), browsers send an OPTIONS request to check permissions.

- **Headers Used:**
  - **`Access-Control-Allow-Origin:`** Specifies which domains are allowed.
  - **`Access-Control-Allow-Methods:`** Specifies which HTTP methods are allowed.
  - **`Access-Control-Allow-Headers:`** Specifies which headers can be used in requests.

**Example:**

**Server Response Headers:**

```http
Access-Control-Allow-Origin: https://example.com
```

**Client Request:**

```javascript
fetch("https://api.example.com/data")
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

**Explanation:**

- **Server Side:** Configures headers to allow requests from specific domains.
- **Client Side:** The browser checks CORS headers and either allows or blocks the request based on the server's response.

---

### **9. What are security considerations like XSS and CSRF?**

**Explanation:**

**XSS (Cross-Site Scripting):** An attack where an attacker injects malicious scripts into webpages viewed by other users.

- **Types of XSS:**

  - **Stored XSS:** Malicious script is stored on the server and served to users.
  - **Reflected XSS:** Malicious script is reflected off a server, like in URL parameters.

- **Prevention:**
  - **Sanitize Inputs:** Ensure user inputs are clean.
  - **Escape Outputs:** Encode data before rendering on the page.

**CSRF (Cross-Site Request Forgery):** An attack where unauthorized commands are sent from a user that the web application trusts.

- **How It Works:**

  - An attacker tricks the user into submitting a request to another site where the user is authenticated.

- **Prevention:**
  - **CSRF Tokens:** Include unique tokens in forms to verify requests.
  - **SameSite Cookies:** Restrict cookies from being sent with cross-site requests.

**Example of CSRF Prevention:**

```html
<form method="POST" action="/update">
  <input type="hidden" name="csrfToken" value="unique_token" />
  <button type="submit">Update</button>
</form>
```

**Explanation:**

- **XSS:** Properly handle user inputs and outputs to avoid script injection.
- **CSRF:** Use tokens and cookie attributes to prevent unauthorized requests.

---

### **10. How do local storage and session storage work, and what are their methods?**

**Explanation:**

**Local Storage** and **Session Storage** are both part of the Web Storage API that allows storing data on the client side.

- **Local Storage:**

  - **Persistence:** Data persists even after the browser is closed.
  - **Usage:** Suitable for storing data that should be retained across sessions.

- **Session Storage:**

  - **Persistence:** Data is cleared when the page session ends (i.e., when the page is closed).
  - **Usage:** Suitable for storing data that should only be available during a single session.

- **Common Methods:**
  - **`.setItem(key, value)`**: Stores a value.
  - **`.getItem(key)`**: Retrieves a value.
  - **`.removeItem(key)`**: Removes an item.
  - **`.clear()`**: Clears all data.

**Example:**

```javascript
// Local Storage
localStorage.setItem("name", "John");
console.log(localStorage.getItem("name")); // Output: 'John'

// Session Storage
sessionStorage.setItem("sessionName", "Doe");
console.log(sessionStorage.getItem("sessionName")); // Output: 'Doe'
```

**Explanation:**

- **Local Storage** keeps data available across browser sessions.
- **Session Storage** keeps data available only during the current browser session.

---

### **11. What are floats and clearing in CSS?**

**Explanation:**

**Floats** and **clearing** are techniques used in CSS for layout and positioning elements on a webpage.

- **Floats:**

  - **Purpose:** To position an element to the left or right of its container, allowing other content to wrap around it.
  - **Common Uses:** For text wrapping around images or creating multi-column layouts.

  **Example:**

  ```css
  .float-left {
    float: left;
    margin-right: 10px;
  }

  .float-right {
    float: right;
    margin-left: 10px;
  }
  ```

  **HTML:**

  ```html
  <img src="example.jpg" class="float-left" alt="Example" />
  <p>This text will wrap around the floated image.</p>
  ```

  **Explanation:**

  - The image floats to the left, and the text wraps around it.

- **Clearing:**

  - **Purpose:** To control the behavior of elements after floated elements, ensuring that they start below any preceding floated elements.
  - **Common Properties:**
    - **`clear: both;`**: Clears both left and right floats.
    - **`clear: left;`**: Clears left floats.
    - **`clear: right;`**: Clears right floats.

  **Example:**

  ```css
  .clearfix::after {
    content: "";
    display: table;
    clear: both;
  }
  ```

  **HTML:**

  ```html
  <div class="clearfix">
    <img src="example.jpg" class="float-left" alt="Example" />
    <p>This text will wrap around the floated image.</p>
  </div>
  ```

  **Explanation:**

  - The `.clearfix` class ensures that any floating elements inside the container are cleared, so the container expands to include its floated children.

---

### **12. What are CSS preprocessors (e.g., Sass, Less)? What is the importance of the `@import` keyword?**

**Explanation:**

**CSS preprocessors** like **Sass** and **Less** extend CSS with features that make it easier to write and maintain complex stylesheets.

- **Sass:**

  - **Features:**
    - **Variables:** Store values like colors and fonts for reuse.
    - **Nesting:** Nest CSS rules inside one another to reflect HTML structure.
    - **Mixins:** Reusable chunks of code.

  **Example:**

  ```scss
  $primary-color: #333;

  .header {
    color: $primary-color;
    .title {
      font-size: 2em;
    }
  }
  ```

  - **Compilation:** Sass files (`.scss` or `.sass`) are compiled into standard CSS.

- **Less:**

  - **Features:**
    - **Variables:** Similar to Sass for reusing values.
    - **Mixins:** Reusable styles.
    - **Operations:** Perform calculations with values.

  **Example:**

  ```less
  @primary-color: #333;

  .header {
    color: @primary-color;
    .title {
      font-size: 2em;
    }
  }
  ```

  - **Compilation:** Less files (`.less`) are compiled into CSS.

- **Importance of `@import`:**

  - **Usage:** Allows importing CSS or preprocessor files into another file.
  - **Benefits:**
    - **Modularization:** Break down large CSS files into smaller, manageable pieces.
    - **Reusability:** Import common styles across multiple stylesheets.

  **Example:**

  ```scss
  @import "variables";
  @import "mixins";

  .header {
    color: $primary-color;
  }
  ```

  **Explanation:**

  - **`@import`** helps keep stylesheets organized and manageable by importing common files or modules.

---

### **13. What are vendor prefixes, and how do they affect browser compatibility?**

**Explanation:**

**Vendor prefixes** are used to ensure that experimental or non-standard CSS properties work in different browsers.

- **Purpose:** They provide support for new CSS features before they become standardized.

- **Common Prefixes:**

  - **`-webkit-`**: For WebKit-based browsers (e.g., Chrome, Safari).
  - **`-moz-`**: For Mozilla-based browsers (e.g., Firefox).
  - **`-ms-`**: For Microsoft browsers (e.g., Internet Explorer, Edge).
  - **`-o-`**: For Opera.

- **Example:**

  ```css
  .box {
    -webkit-border-radius: 10px; /* Chrome, Safari */
    -moz-border-radius: 10px; /* Firefox */
    border-radius: 10px; /* Standard */
  }
  ```

- **Impact on Compatibility:**
  - **Browser Support:** Prefixes ensure that features are available in browsers that don’t yet support the standard property.
  - **Fallbacks:** Always provide the standard property after the prefixed versions to cover browsers that support the standard.

**Explanation:**

- **Vendor Prefixes** help developers use experimental CSS features while maintaining compatibility with multiple browsers.

---

### **14. What are CSS methodologies (e.g., BEM, SMACSS)?**

**Explanation:**

**CSS methodologies** are approaches to organizing and managing CSS to improve maintainability and scalability.

- **BEM (Block Element Modifier):**

  - **Concept:** Divides CSS into blocks (independent components), elements (parts of blocks), and modifiers (variations).
  - **Naming Convention:** Use a structured naming pattern to avoid conflicts and improve clarity.

  **Example:**

  ```html
  <div class="button button--primary">
    <span class="button__text">Click me</span>
  </div>
  ```

  **CSS:**

  ```css
  .button {
    padding: 10px;
    border: 1px solid #ccc;
  }

  .button--primary {
    background-color: blue;
    color: white;
  }

  .button__text {
    font-size: 16px;
  }
  ```

- **SMACSS (Scalable and Modular Architecture for CSS):**

  - **Concept:** Organizes CSS into categories like Base, Layout, Module, State, and Theme.
  - **Purpose:** Encourages modular and scalable CSS by structuring styles into logical components.

  **Example:**

  ```css
  /* Layout */
  .header {
    ...;
  }

  /* Module */
  .card {
    ...;
  }

  /* State */
  .is-active {
    ...;
  }
  ```

**Explanation:**

- **BEM** provides a clear structure for naming and organizing CSS to avoid conflicts and improve readability.
- **SMACSS** offers a flexible approach to structuring stylesheets for maintainability and scalability.

---

### **15. What are CSS variables (custom properties)?**

**Explanation:**

**CSS variables**, also known as **custom properties**, allow you to store and reuse values throughout your CSS.

- **Definition:** Variables defined using the `--` prefix, and used with the `var()` function.

- **Creation and Usage:**

  - **Define Variables:**

    ```css
    :root {
      --main-color: #3498db;
      --padding: 10px;
    }
    ```

  - **Use Variables:**
    ```css
    .box {
      background-color: var(--main-color);
      padding: var(--padding);
    }
    ```

- **Benefits:**

  - **Reusability:** Use the same value throughout your stylesheets.
  - **Maintainability:** Easily update the value in one place.
  - **Dynamic Changes:** Variables can be changed using JavaScript.

  **Example:**

  ```javascript
  document.documentElement.style.setProperty("--main-color", "#e74c3c");
  ```

**Explanation:**

- **CSS Variables** provide a way to define reusable values that can be changed dynamically, improving maintainability and flexibility in your stylesheets.

---

### **16. Is `useState` scheduled? If yes, why? What is `useState`'s `prevState`?**

**Explanation:**

In React, **`useState`** is a hook that lets you add state to functional components.

- **Is `useState` Scheduled?**

  - **Scheduling:** React schedules state updates to be processed in batches for performance reasons. This means that updates may not happen immediately but will be applied in the next render cycle.

- **Why Scheduling:**

  - **Performance:** Batch updates reduce the number of re-renders and improve application performance.

- **What is `prevState`:**

  - **`prevState`** is used to access the previous state value when updating state. This is crucial when updating state based on the previous value.

  **Example:**

  ```javascript
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount((prevCount) => prevCount + 1);
  };
  ```

  **Explanation:**

  - **`prevState` Function:** Ensures you get the latest state value when updating, preventing issues with stale state in asynchronous updates.

---

### **17. Why is a `useState` variable declared as a constant but still mutable?**

**Explanation:**

**`useState`** returns an array with two elements: the current state value and a function to update that value. The state itself is mutable, but

the state variable is declared as a constant.

- **Constant Declaration:**

  - The `const` keyword ensures that the reference to the `useState` hook’s return value cannot be reassigned, meaning you cannot change what `count` refers to.

- **Mutable Nature of State:**

  - Although `count` is a constant reference, the state value it holds can be updated using the updater function (`setCount`).

  **Example:**

  ```javascript
  const [count, setCount] = useState(0);

  // count is a constant reference, but its value can be updated
  setCount(count + 1);
  ```

**Explanation:**

- **`const`** ensures the reference to the state value doesn’t change, but the state itself is mutable through the updater function.

---

### **18. Why is React Router used?**

**Explanation:**

**React Router** is a library used for handling routing in React applications, enabling navigation between different components or pages.

- **Purpose:**

  - **Single Page Applications (SPAs):** Manage navigation without reloading the page.
  - **Dynamic Routing:** Define routes based on the application’s state or URL parameters.

- **Benefits:**

  - **Declarative Routing:** Define routes using React components.
  - **Nested Routing:** Create nested routes for complex layouts.

  **Example:**

  ```javascript
  import { BrowserRouter as Router, Route, Switch } from "react-router-dom";

  function App() {
    return (
      <Router>
        <Switch>
          <Route path="/" exact component={Home} />
          <Route path="/about" component={About} />
        </Switch>
      </Router>
    );
  }
  ```

**Explanation:**

- **React Router** simplifies routing in SPAs, allowing developers to define routes as React components and manage navigation without page reloads.

---

### **19. What does the `index` keyword do in React Router?**

**Explanation:**

In **React Router**, the **`index`** keyword is used in the context of nested routes to define the default route within a parent route.

- **Purpose:**

  - **Index Route:** Specifies which component should be rendered when the parent route is matched but no child routes are specified.

  **Example:**

  ```javascript
  import { Route, Routes } from "react-router-dom";

  function App() {
    return (
      <Routes>
        <Route path="/" element={<Layout />}>
          <Route index element={<Home />} /> {/* Index route */}
          <Route path="about" element={<About />} />
        </Route>
      </Routes>
    );
  }
  ```

**Explanation:**

- **Index Route** renders the specified component (`<Home />`) when the parent route (`"/"`) is matched, providing a default view.

---

### **20. What is the `some()` method in JavaScript?**

**Explanation:**

The **`some()`** method is an array method in JavaScript that tests whether at least one element in the array passes a test provided by a function.

- **Syntax:**

  ```javascript
  array.some(callback(element, index, array));
  ```

- **Parameters:**

  - **`callback`**: A function that tests each element. It returns `true` if the test passes, `false` otherwise.

- **Returns:**
  - **`true`** if at least one element passes the test.
  - **`false`** if no elements pass the test.

**Example:**

```javascript
const numbers = [1, 2, 3, 4, 5];
const hasEven = numbers.some((num) => num % 2 === 0);
console.log(hasEven); // Output: true
```

**Explanation:**

- **`some()`** checks if there’s at least one even number in the array and returns `true` if so.

---

### **21. What is the `useRef()` hook in React?**

**Explanation:**

The **`useRef()`** hook is used to create a mutable reference that persists across re-renders in a functional component.

- **Purpose:**

  - **Access DOM Elements:** Get direct access to DOM elements.
  - **Store Mutable Values:** Keep mutable values that don’t trigger re-renders.

- **Usage:**

  - **DOM Access:**

    ```javascript
    const inputRef = useRef(null);

    useEffect(() => {
      inputRef.current.focus();
    }, []);
    ```

  - **Storing Values:**

    ```javascript
    const countRef = useRef(0);

    const increment = () => {
      countRef.current += 1;
      console.log(countRef.current);
    };
    ```

**Explanation:**

- **`useRef()`** provides a way to persist values across renders without causing re-renders, making it useful for accessing DOM elements and storing mutable values.

---

### **22. What is the `useOnClickOutside()` hook in React?**

**Explanation:**

The **`useOnClickOutside()`** hook is a custom hook used to detect clicks outside of a specified element, useful for handling click events that close modals or dropdowns.

- **Purpose:**

  - **Detect Outside Clicks:** Trigger an action when a user clicks outside a specified element.

- **Implementation:**

  - **Example Hook:**

    ```javascript
    import { useEffect } from "react";

    function useOnClickOutside(ref, handler) {
      useEffect(() => {
        const handleClick = (event) => {
          if (ref.current && !ref.current.contains(event.target)) {
            handler(event);
          }
        };

        document.addEventListener("mousedown", handleClick);
        return () => document.removeEventListener("mousedown", handleClick);
      }, [ref, handler]);
    }
    ```

  - **Usage:**

    ```javascript
    const ref = useRef();

    useOnClickOutside(ref, () => {
      console.log("Clicked outside!");
    });
    ```

**Explanation:**

- **`useOnClickOutside()`** helps in implementing features like closing dropdowns or modals when a user clicks outside of them.

---

### **23. What is the `useSelector()` hook in React?**

**Explanation:**

The **`useSelector()`** hook is a part of the React-Redux library that allows you to access the Redux store’s state in functional components.

- **Purpose:**

  - **Access Redux State:** Retrieve specific pieces of state from the Redux store.

- **Usage:**

  - **Example:**

    ```javascript
    import { useSelector } from "react-redux";

    function MyComponent() {
      const count = useSelector((state) => state.counter);
      return <div>Count: {count}</div>;
    }
    ```

**Explanation:**

- **`useSelector()`** allows components to read values from the Redux store and re-render when the selected state changes.

---

### **24. What is the `useDispatch()` hook in React?**

**Explanation:**

The **`useDispatch()`** hook is a part of the React-Redux library used to dispatch actions to the Redux store.

- **Purpose:**

  - **Dispatch Actions:** Send actions to update the Redux store’s state.

- **Usage:**

  - **Example:**

    ```javascript
    import { useDispatch } from "react-redux";
    import { increment } from "./actions";

    function Counter() {
      const dispatch = useDispatch();

      const handleIncrement = () => {
        dispatch(increment());
      };

      return <button onClick={handleIncrement}>Increment</button>;
    }
    ```

**Explanation:**

- **`useDispatch()`** provides a way to send actions to the Redux store, triggering state updates.

---

### **25. How does the `useEffect()` hook work, and what is its cleanup function?**

**Explanation:**

The **`useEffect()`** hook in React is used to perform side effects in functional components. Side effects include data fetching, subscriptions, and manual DOM manipulations.

- **Purpose:**

  - **Perform Side Effects:** Execute code that interacts with outside systems or APIs.

- **Usage:**

  - **Basic Syntax:**

    ```javascript
    useEffect(() => {
      // Side effect code here

      return () => {
        // Cleanup code here
      };
    }, [dependencies]);
    ```

- **Cleanup Function:**

  - **Purpose:** Used to clean up resources like subscriptions or timers before the component is removed or before the effect runs again.
  - **Usage:**

    ```javascript
    useEffect(() => {
      const timer = setInterval(() => {
        console.log("Tick");
      }, 1000);

      return () => clearInterval(timer); // Cleanup timer
    }, []);
    ```

**Explanation:**

- **`useEffect()`** executes after the render and handles side effects. The cleanup function ensures resources are properly released.

---

### **26. What are the `useCallback` and `useMemo` hooks in React?**

**Explanation:**

- **`useCallback()`**:

  - **Purpose:** Memoize functions to prevent re-creation on every render. Useful when passing callbacks to child components to avoid unnecessary re-renders.
  - **Usage:**

    ```javascript
    import { useCallback } from "react";

    const MyComponent = () => {
      const handleClick = useCallback(() => {
        console.log("Button clicked");
      }, []); // Dependency array

      return <button onClick={handleClick}>Click Me</button>;
    };
    ```

  **Explanation:**

  - **`useCallback()`** keeps the function reference stable between renders

unless its dependencies change.

- **`useMemo()`**:

  - **Purpose:** Memoize values to avoid recalculating them on every render.
  - **Usage:**

    ```javascript
    import { useMemo } from "react";

    const MyComponent = ({ items }) => {
      const sortedItems = useMemo(() => {
        return items.sort();
      }, [items]);

      return (
        <ul>
          {sortedItems.map((item) => (
            <li key={item}>{item}</li>
          ))}
        </ul>
      );
    };
    ```

  **Explanation:**

  - **`useMemo()`** caches the result of a computation and only recalculates it when dependencies change.

---

### **27. What is the Context API, and how do its hooks work?**

**Explanation:**

The **Context API** in React is used for managing global state or passing data through the component tree without prop drilling.

- **Components:**

  - **`React.createContext()`**: Creates a Context object.
  - **`Context.Provider`**: Provides the context value to child components.
  - **`Context.Consumer`**: Consumes the context value in a class component (or `useContext()` in functional components).

- **Usage:**

  - **Create Context:**

    ```javascript
    const MyContext = React.createContext();
    ```

  - **Provider:**

    ```javascript
    <MyContext.Provider value={someValue}>
      <ChildComponent />
    </MyContext.Provider>
    ```

  - **Consumer with Hook:**

    ```javascript
    import { useContext } from "react";

    function ChildComponent() {
      const contextValue = useContext(MyContext);
      return <div>{contextValue}</div>;
    }
    ```

**Explanation:**

- **Context API** allows sharing values across components without passing props explicitly, improving code readability and component composition.

---

### **28. What is Redux Toolkit, and how do slices and store work in it?**

**Explanation:**

**Redux Toolkit** is a set of tools and best practices for writing Redux logic more efficiently and with less boilerplate.

- **Features:**

  - **`createSlice`**: Defines reducers and actions in a single slice.
  - **`configureStore`**: Sets up the Redux store with sensible defaults.

- **Usage:**

  - **Create Slice:**

    ```javascript
    import { createSlice } from "@reduxjs/toolkit";

    const counterSlice = createSlice({
      name: "counter",
      initialState: 0,
      reducers: {
        increment: (state) => state + 1,
        decrement: (state) => state - 1,
      },
    });

    export const { increment, decrement } = counterSlice.actions;
    export default counterSlice.reducer;
    ```

  - **Configure Store:**

    ```javascript
    import { configureStore } from "@reduxjs/toolkit";
    import counterReducer from "./counterSlice";

    const store = configureStore({
      reducer: {
        counter: counterReducer,
      },
    });

    export default store;
    ```

**Explanation:**

- **Redux Toolkit** simplifies Redux development by providing a streamlined API for creating slices and configuring the store.

---

### **29. What are the `useLocation()` and `useSearchParams()` hooks in React Router?**

**Explanation:**

- **`useLocation()`**:

  - **Purpose:** Access the current location object, including the pathname, search, and hash.
  - **Usage:**

    ```javascript
    import { useLocation } from "react-router-dom";

    function MyComponent() {
      const location = useLocation();
      return <div>Current path: {location.pathname}</div>;
    }
    ```

  **Explanation:**

  - **`useLocation()`** provides information about the current URL, useful for displaying or reacting to location changes.

- **`useSearchParams()`**:

  - **Purpose:** Manage and access URL query parameters.
  - **Usage:**

    ```javascript
    import { useSearchParams } from "react-router-dom";

    function MyComponent() {
      const [searchParams, setSearchParams] = useSearchParams();
      const page = searchParams.get("page") || 1;

      return (
        <div>
          <p>Current page: {page}</p>
          <button onClick={() => setSearchParams({ page: Number(page) + 1 })}>
            Next Page
          </button>
        </div>
      );
    }
    ```

  **Explanation:**

  - **`useSearchParams()`** allows managing query parameters in the URL, enabling dynamic query-based navigation.

---

### **30. What is `useParams()` in React Router?**

**Explanation:**

The **`useParams()`** hook in React Router provides access to route parameters in functional components.

- **Purpose:**

  - **Access Route Parameters:** Retrieve dynamic segments of the URL defined in the route configuration.

- **Usage:**

  - **Example:**

    ```javascript
    import { useParams } from "react-router-dom";

    function UserProfile() {
      const { userId } = useParams();
      return <div>User ID: {userId}</div>;
    }
    ```

  **Explanation:**

  - **`useParams()`** extracts route parameters, such as `userId` from the URL, making them available in the component.

---

### **31. What are the libraries `three.js` and `chart.js` used for?**

**Explanation:**

- **`three.js`:**

  - **Purpose:** A library for creating and rendering 3D graphics in the browser using WebGL.
  - **Features:**
    - **3D Rendering:** Create 3D scenes, objects, and animations.
    - **Lighting and Materials:** Apply different lighting and materials to objects.

  **Example:**

  ```javascript
  import * as THREE from "three";

  const scene = new THREE.Scene();
  const camera = new THREE.PerspectiveCamera(
    75,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
  );
  const renderer = new THREE.WebGLRenderer();

  renderer.setSize(window.innerWidth, window.innerHeight);
  document.body.appendChild(renderer.domElement);

  const geometry = new THREE.BoxGeometry();
  const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
  const cube = new THREE.Mesh(geometry, material);

  scene.add(cube);
  camera.position.z = 5;

  function animate() {
    requestAnimationFrame(animate);
    cube.rotation.x += 0.01;
    cube.rotation.y += 0.01;
    renderer.render(scene, camera);
  }

  animate();
  ```

  **Explanation:**

  - **`three.js`** is used to create interactive 3D graphics and animations in web applications.

- **`chart.js`:**

  - **Purpose:** A library for creating various types of charts and graphs.
  - **Features:**
    - **Chart Types:** Line, bar, pie, radar, and more.
    - **Customization:** Highly customizable chart appearance and behavior.

  **Example:**

  ```javascript
  import Chart from "chart.js/auto";

  const ctx = document.getElementById("myChart").getContext("2d");
  new Chart(ctx, {
    type: "bar",
    data: {
      labels: ["Red", "Blue", "Yellow", "Green", "Purple", "Orange"],
      datasets: [
        {
          label: "# of Votes",
          data: [12, 19, 3, 5, 2, 3],
          backgroundColor: [
            "rgba(255, 99, 132, 0.2)",
            "rgba(54, 162, 235, 0.2)",
            "rgba(255, 206, 86, 0.2)",
            "rgba(75, 192, 192, 0.2)",
            "rgba(153, 102, 255, 0.2)",
            "rgba(255, 159, 64, 0.2)",
          ],
          borderColor: [
            "rgba(255, 99, 132, 1)",
            "rgba(54, 162, 235, 1)",
            "rgba(255, 206, 86, 1)",
            "rgba(75, 192, 192, 1)",
            "rgba(153, 102, 255, 1)",
            "rgba(255, 159, 64, 1)",
          ],
          borderWidth: 1,
        },
      ],
    },
    options: {
      scales: {
        y: {
          beginAtZero: true,
        },
      },
    },
  });
  ```

  **Explanation:**

  - **`chart.js`** simplifies the process of creating and customizing charts for data visualization in web applications.

---

### **32. How do CORS and Axios work together?**

**Explanation:**

**CORS (Cross-Origin Resource Sharing)** and **Axios** are used together when making HTTP requests to handle cross-origin restrictions.

- **CORS:**

  - **Purpose:** A security feature in browsers to restrict web pages from making requests to a different origin than the one that served the web page.
  - **How It Works:** Servers must include specific headers to allow cross-origin requests, such as `Access-Control-Allow-Origin`.

- **Axios:**

  - **Purpose:** A popular HTTP client library for making requests from the browser or Node.js.
  - **Usage with CORS:**
    - **Setup:** Axios sends HTTP requests with necessary headers, and the server must handle CORS properly.

  \*\*

Example:\*\*

```javascript
import axios from "axios";

axios
  .get("https://api.example.com/data")
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error fetching data:", error);
  });
```

**Explanation:**

- **Axios** can make HTTP requests across different origins, but **CORS** policies on the server determine if the request is allowed.

---

### **33. What is the `next()` function in Express.js?**

**Explanation:**

The **`next()`** function in **Express.js** is used to pass control to the next middleware function in the stack.

- **Purpose:**

  - **Middleware Flow:** Ensure that multiple middleware functions are executed in sequence.
  - **Error Handling:** Pass errors to error-handling middleware.

- **Usage:**

  - **Basic Middleware:**

    ```javascript
    app.use((req, res, next) => {
      console.log("Middleware 1");
      next(); // Pass control to the next middleware
    });

    app.use((req, res, next) => {
      console.log("Middleware 2");
      res.send("Response from second middleware");
    });
    ```

  - **Error Handling:**
    ```javascript
    app.use((err, req, res, next) => {
      console.error(err.stack);
      res.status(500).send("Something broke!");
    });
    ```

**Explanation:**

- **`next()`** is crucial for managing the flow of request handling in Express.js, allowing you to build complex middleware chains and error-handling mechanisms.

---

### **34. What is the `req.body` object in Express.js?**

**Explanation:**

In **Express.js**, the **`req.body`** object contains data sent in the body of the request, typically from POST or PUT requests.

- **Purpose:**

  - **Data Access:** Access form data or JSON payloads sent in the body of the request.

- **Usage:**

  - **Middleware Setup:**

    - **JSON Body Parsing:**

      ```javascript
      const express = require("express");
      const app = express();

      app.use(express.json()); // Middleware to parse JSON bodies

      app.post("/data", (req, res) => {
        console.log(req.body); // Access body data
        res.send("Data received");
      });
      ```

  - **Form Data:**

    ```javascript
    app.use(express.urlencoded({ extended: true })); // Middleware to parse URL-encoded bodies

    app.post("/form", (req, res) => {
      console.log(req.body); // Access form data
      res.send("Form data received");
    });
    ```

**Explanation:**

- **`req.body`** is used to access data sent by the client in the request body, allowing you to handle form submissions, JSON payloads, and other data.

---

### **35. How do `async` and `await` work in JavaScript?**

**Explanation:**

**`async`** and **`await`** are syntax features in JavaScript that simplify working with asynchronous code, making it easier to read and write.

- **`async` Function:**

  - **Purpose:** Declares a function that returns a Promise. It allows the use of **`await`** inside the function.
  - **Usage:**
    ```javascript
    async function fetchData() {
      const response = await fetch("https://api.example.com/data");
      const data = await response.json();
      return data;
    }
    ```

- **`await` Expression:**
  - **Purpose:** Pauses the execution of the `async` function until the Promise is resolved, making the code appear synchronous.
  - **Usage:**
    ```javascript
    async function getData() {
      try {
        const data = await fetchData();
        console.log(data);
      } catch (error) {
        console.error("Error:", error);
      }
    }
    ```

**Explanation:**

- **`async`** and **`await`** simplify handling asynchronous operations by allowing code to be written in a more synchronous style, improving readability and error handling.

---

### **36. What is a WebSocket, and how is it used in JavaScript?**

**Explanation:**

**WebSocket** is a protocol for full-duplex communication channels over a single TCP connection, enabling real-time data exchange between a client and server.

- **Purpose:**

  - **Real-Time Communication:** Enable bidirectional, real-time communication, such as chat applications or live updates.

- **Usage:**

  - **JavaScript Example:**

    ```javascript
    const socket = new WebSocket("ws://example.com/socket");

    socket.onopen = () => {
      console.log("Connected to WebSocket");
      socket.send("Hello Server!");
    };

    socket.onmessage = (event) => {
      console.log("Message from server:", event.data);
    };

    socket.onerror = (error) => {
      console.error("WebSocket error:", error);
    };

    socket.onclose = () => {
      console.log("WebSocket connection closed");
    };
    ```

**Explanation:**

- **WebSocket** provides a persistent connection that allows real-time, interactive communication between clients and servers, ideal for applications requiring constant data exchange.

---

### **37. What is JSON, and why is it used?**

**Explanation:**

**JSON** (JavaScript Object Notation) is a lightweight data interchange format that is easy for humans to read and write and easy for machines to parse and generate.

- **Purpose:**

  - **Data Exchange:** Commonly used for exchanging data between a server and a web application.
  - **Serialization:** Convert data structures or objects into a string format that can be easily transmitted.

- **Structure:**

  - **Objects:** `{ "key": "value" }`
  - **Arrays:** `[ "value1", "value2" ]`
  - **Data Types:** Strings, numbers, booleans, arrays, objects, and `null`.

- **Usage Example:**

  ```javascript
  const user = {
    name: "John Doe",
    age: 30,
    isActive: true,
    address: {
      street: "123 Main St",
      city: "Anytown",
    },
    hobbies: ["reading", "gaming"],
  };

  // Convert object to JSON string
  const jsonString = JSON.stringify(user);
  console.log(jsonString);

  // Convert JSON string back to object
  const jsonObject = JSON.parse(jsonString);
  console.log(jsonObject);
  ```

**Explanation:**

- **JSON** is widely used because it is simple, language-independent, and works seamlessly with JavaScript and other programming languages.

---

### **38. What is the difference between DOM and BOM in JavaScript?**

**Explanation:**

- **DOM (Document Object Model):**

  - **Purpose:** Represents the structure of an HTML document as a tree of objects, allowing JavaScript to interact with and manipulate the content and structure of web pages.
  - **Example:**
    ```javascript
    // Accessing an element by its ID
    const element = document.getElementById("myElement");
    element.textContent = "New content";
    ```

- **BOM (Browser Object Model):**

  - **Purpose:** Provides interaction with the browser's components, such as the window, navigator, and history objects. It allows JavaScript to control browser-specific features and handle browser events.
  - **Example:**

    ```javascript
    // Accessing the window object
    console.log(window.location.href);

    // Using the history object
    window.history.back();
    ```

**Explanation:**

- **DOM** focuses on the document's structure, while **BOM** deals with the browser's environment and functionalities.

---

### **39. What is the window object in JavaScript?**

**Explanation:**

The **`window`** object represents the browser window and provides access to various properties and methods related to the browser.

- **Properties:**

  - **`window.location`:** Provides information about the current URL.
  - **`window.document`:** Refers to the DOM of the current document.
  - **`window.history`:** Allows manipulation of the browser history.

- **Methods:**
  - **`window.alert()`:** Displays an alert dialog.
  - **`window.open()`:** Opens a new browser window.

**Usage Example:**

```javascript
// Display an alert message
window.alert("Hello, world!");

// Get current URL
const currentURL = window.location.href;
console.log(currentURL);
```

**Explanation:**

- The **`window`** object is the global object in the browser environment, providing various properties and methods to interact with the web page and the browser.

---

### **40. What are the phases of events in JavaScript?**

**Explanation:**

Events in JavaScript go through several phases during their lifecycle:

1. **Capturing Phase:**

   - **Description:** The event starts from the top of the DOM hierarchy and travels down to the target element.
   - **Usage:** Rarely used; you can listen for events during this phase by setting the `capture` parameter to `true`.

2. **Target Phase:**

   - **Description:** The event is dispatched to the target element where it was actually triggered.

3. **Bubbling Phase:**
   - **Description:** The event bubbles up from the target element to the top of the DOM hierarchy.
   - **Usage:** Commonly used; allows parent elements to respond to events triggered by their children.

**Usage Example:**

```javascript
document.getElementById("myButton").addEventListener(
  "click",
  (event) => {
    console.log("Button clicked");
  },
  true
); // `true` for capturing phase, `false` for bubbling phase
```

**Explanation:**

- **Event Phases** determine how events propagate through the DOM, allowing fine-grained control over event handling.

---

### **41. What is `flushSync()` in React?**

**Explanation:**

**`flushSync()`** is a React API used to force a synchronous update of the React state. This can be useful in scenarios where you need to ensure that the DOM updates immediately.

- **Usage Example:**

  ```javascript
  import React, { useState, flushSync } from "react";

  function MyComponent() {
    const [count, setCount] = useState(0);

    const handleClick = () => {
      flushSync(() => {
        setCount(count + 1);
      });
      console.log("Count updated synchronously");
    };

    return <button onClick={handleClick}>{count}</button>;
  }
  ```

**Explanation:**

- **`flushSync()`** ensures that the state updates are immediately reflected in the DOM, bypassing React's asynchronous batching.

---

### **42. What is a React Fragment, and how can you write it in different ways?**

**Explanation:**

A **React Fragment** is a wrapper component that allows grouping multiple elements without adding extra nodes to the DOM.

- **Usage Example:**

  - **Using `<React.Fragment>`:**

    ```javascript
    function MyComponent() {
      return (
        <React.Fragment>
          <h1>Hello</h1>
          <p>World</p>
        </React.Fragment>
      );
    }
    ```

  - **Using Short Syntax `<>` and `</>`:**
    ```javascript
    function MyComponent() {
      return (
        <>
          <h1>Hello</h1>
          <p>World</p>
        </>
      );
    }
    ```

**Explanation:**

- **React Fragments** help to group elements without adding extra markup, which can be useful for improving the structure of your JSX without affecting the DOM.

---

### **43. What does the `eval()` method do in JavaScript?**

**Explanation:**

The **`eval()`** function evaluates a string as JavaScript code and executes it.

- **Usage Example:**
  ```javascript
  const code = "2 + 2";
  console.log(eval(code)); // Outputs: 4
  ```

**Risks:**

- **Security Risks:** Can execute arbitrary code, which might lead to security vulnerabilities.
- **Performance Impact:** Can affect performance due to the dynamic nature of code execution.

**Explanation:**

- **`eval()`** should be used cautiously due to potential security and performance issues. It's often better to avoid using it and find safer alternatives.

---

### **44. What is a prop function in React?**

**Explanation:**

A **prop function** is a function passed as a prop from a parent component to a child component, allowing the parent to pass down functionality to the child.

- **Usage Example:**

  ```javascript
  function ParentComponent() {
    const handleClick = () => {
      console.log("Button clicked");
    };

    return <ChildComponent onClick={handleClick} />;
  }

  function ChildComponent({ onClick }) {
    return <button onClick={onClick}>Click me</button>;
  }
  ```

**Explanation:**

- **Prop functions** allow for customizable interactions between components, making your components more reusable and composable.

---

### **45. What is a controlled component in React?**

**Explanation:**

A **controlled component** is an input element whose value is controlled by React state.

- **Usage Example:**

  ```javascript
  function MyForm() {
    const [value, setValue] = useState("");

    const handleChange = (event) => {
      setValue(event.target.value);
    };

    return <input type="text" value={value} onChange={handleChange} />;
  }
  ```

**Explanation:**

- **Controlled components** give you more control over form elements by allowing you to manage their state in React, making it easier to handle user inputs and form submissions.

---

### **46. What is React Router DOM?**

**Explanation:**

**React Router DOM** is a library used for routing in React applications. It allows you to define routes in your app and manage navigation between different components or pages.

- **Usage Example:**

  ```javascript
  import { BrowserRouter as Router, Route, Switch } from "react-router-dom";

  function App() {
    return (
      <Router>
        <Switch>
          <Route path="/home" component={HomePage} />
          <Route path="/about" component={AboutPage} />
          <Route path="/" component={MainPage} />
        </Switch>
      </Router>
    );
  }
  ```

**Explanation:**

- **React Router DOM** simplifies managing navigation and routing in React applications, allowing for a more dynamic and interactive user experience.

---

### **47. What is hoisting in JavaScript for functions and variables?**

**Explanation:**

**Hoisting** is a JavaScript behavior where variable and function

declarations are moved to the top of their containing scope during compilation.

- **Variables:**

  - **`var`** declarations are hoisted and initialized to `undefined`.
  - **`let`** and **`const`** declarations are hoisted but not initialized; accessing them before declaration results in a `ReferenceError`.

- **Functions:**
  - Function declarations are hoisted along with their definitions, so you can call them before their declaration in the code.

**Usage Example:**

```javascript
console.log(x); // Outputs: undefined
var x = 5;

foo(); // Outputs: "Hello"
function foo() {
  console.log("Hello");
}
```

**Explanation:**

- **Hoisting** allows for flexible coding practices, but understanding how it works can help prevent unexpected behavior and bugs.

---

### **48. What are scopes in JavaScript, and what is lexical scoping?**

**Explanation:**

**Scope** determines the visibility of variables and functions in different parts of your code.

- **Global Scope:** Variables declared outside of functions are in the global scope and accessible anywhere.
- **Function Scope:** Variables declared within a function are only accessible inside that function.

**Lexical Scoping:** Refers to how variable scope is determined based on the location where variables are declared. Inner functions have access to variables from outer functions.

**Usage Example:**

```javascript
function outerFunction() {
  const outerVar = "I am outside";

  function innerFunction() {
    console.log(outerVar); // Accesses outerVar due to lexical scoping
  }

  innerFunction();
}

outerFunction();
```

**Explanation:**

- **Lexical scoping** ensures that nested functions have access to variables from their parent functions, which is fundamental to JavaScript's function scope.

---

### **49. What is closure in JavaScript, and what is the difference between closure and lexical scoping?**

**Explanation:**

**Closure** is a feature where a function retains access to its lexical scope even after it has finished executing.

- **Usage Example:**

  ```javascript
  function createCounter() {
    let count = 0;

    return function () {
      count += 1;
      return count;
    };
  }

  const counter = createCounter();
  console.log(counter()); // Outputs: 1
  console.log(counter()); // Outputs: 2
  ```

**Difference from Lexical Scoping:**

- **Lexical Scoping** determines the visibility of variables based on their location in the code.
- **Closure** allows functions to retain access to variables from their containing scope even after the outer function has completed.

**Explanation:**

- **Closures** are useful for creating private variables and functions, enabling more powerful and flexible code structures.

---

### **50. Why is `Route` in React Router nested under `Routes`?**

**Explanation:**

In **React Router v6**, the **`Routes`** component is used to group **`Route`** components and provide a more structured and efficient way to define and manage routes.

- **Usage Example:**

  ```javascript
  import { Routes, Route } from "react-router-dom";

  function App() {
    return (
      <Routes>
        <Route path="/home" element={<HomePage />} />
        <Route path="/about" element={<AboutPage />} />
        <Route path="/" element={<MainPage />} />
      </Routes>
    );
  }
  ```

**Explanation:**

- **`Routes`** is a container that handles the matching of routes and rendering of components. This helps in organizing routes and managing nested routing more effectively.

---

### **51. What is the difference between `redirect` and `navigate()` in React Router?**

**Explanation:**

- **`redirect`:**

  - **Purpose:** Used to redirect users to a different route.
  - **Usage (React Router v5):**

    ```javascript
    import { Redirect } from "react-router-dom";

    function MyComponent() {
      return <Redirect to="/home" />;
    }
    ```

- **`navigate()`:**

  - **Purpose:** Provides programmatic navigation to different routes.
  - **Usage (React Router v6):**

    ```javascript
    import { useNavigate } from "react-router-dom";

    function MyComponent() {
      const navigate = useNavigate();

      const handleClick = () => {
        navigate("/home");
      };

      return <button onClick={handleClick}>Go to Home</button>;
    }
    ```

**Explanation:**

- **`redirect`** is a declarative way to navigate, while **`navigate()`** provides a programmatic approach to routing in React Router.

---

### **52. How does the parent route work in React Router, and how are child routes handled?**

**Explanation:**

**Parent routes** define a base route and can contain child routes that render components within the parent route's context.

- **Usage Example:**

  ```javascript
  import { Routes, Route } from "react-router-dom";

  function ParentComponent() {
    return (
      <Routes>
        <Route path="/parent" element={<ParentPage />}>
          <Route path="child1" element={<ChildPage1 />} />
          <Route path="child2" element={<ChildPage2 />} />
        </Route>
      </Routes>
    );
  }
  ```

**Explanation:**

- **Child routes** are nested under parent routes, allowing for more granular control over rendering and route matching. This enables creating hierarchical routing structures.

---

### **53. How does Redux Toolkit work internally?**

**Explanation:**

**Redux Toolkit** is a library that simplifies Redux state management with a set of utilities and best practices.

- **Key Features:**
  - **`createSlice`:** Defines reducers and actions in one place.
  - **`configureStore`:** Sets up the Redux store with sensible defaults.
  - **`createAsyncThunk`:** Handles asynchronous logic with a simple API.

**Usage Example:**

```javascript
import { createSlice, configureStore } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: 0,
  reducers: {
    increment: (state) => state + 1,
    decrement: (state) => state - 1,
  },
});

const store = configureStore({
  reducer: counterSlice.reducer,
});
```

**Explanation:**

- **Redux Toolkit** abstracts much of the boilerplate code and provides a more streamlined way to manage Redux state, making it easier to work with.

---

### **54. Why is a bearer token more secure than using cookies and body parsers?**

**Explanation:**

**Bearer tokens** are used for authentication and are included in HTTP headers. They provide better security compared to cookies and body parsers.

- **Advantages:**
  - **Less Susceptible to CSRF:** Since bearer tokens are included in the Authorization header, they are not vulnerable to Cross-Site Request Forgery (CSRF) attacks.
  - **More Control:** Tokens can be easily invalidated or rotated.

**Usage Example:**

```javascript
fetch("https://api.example.com/data", {
  method: "GET",
  headers: {
    Authorization: `Bearer ${token}`,
  },
});
```

**Explanation:**

- **Bearer tokens** improve security by avoiding common vulnerabilities associated with cookies and body parsers, such as CSRF attacks.

---

### **55. Why is fetching a token from the header more secure than from the body or cookies?**

**Explanation:**

**Fetching tokens from HTTP headers** is generally more secure than from the body or cookies due to several reasons:

- **Headers are Not Accessible via JavaScript:** Tokens in headers are not accessible from JavaScript running on the client-side, reducing the risk of XSS attacks.
- **Avoids CSRF Risks:** Using headers avoids the risks of Cross-Site Request Forgery (CSRF) because headers are not automatically sent with cross-origin requests.

**Usage Example:**

```javascript
fetch("https://api.example.com/data", {
  method: "GET",
  headers: {
    Authorization: `Bearer ${token}`,
  },
});
```

**Explanation:**

- Fetching tokens from headers enhances security by protecting tokens from being exposed to client-side scripts and cross-site attacks.

---

### **56. What are the various methods of JWT, and what is the significance of `saltRound`?**

**Explanation:**

**JWT (JSON Web Token)** methods include:

- **`HS256`:** HMAC using SHA-256, a symmetric key algorithm.
- **`RS256`:** RSA Signature with SHA-256, an asymmetric key algorithm.
- **`ES256`:** ECDSA using P-256 and SHA-256, an elliptic curve algorithm.

**`saltRound`** is related to password hashing and not directly to JWT. It refers to the number of rounds used to generate a salted hash, which adds security to password storage.

**Usage Example for JWT:**

```javascript
const jwt = require("jsonwebtoken");
const token = jwt.sign({ id: userId }, "secretKey", { algorithm: "HS256" });
```

**Explanation:**

- **JWT** provides methods for secure token generation and verification, while **saltRound** enhances password hashing security.

---

### **57. What are Mongoose methods?**

**Explanation:**

**Mongoose** is an ODM (Object Data Modeling) library for MongoDB and Node.js, providing methods to interact with MongoDB collections.

- **Common Methods:**
  - **`find()`:** Retrieves documents based on criteria.
  - **`findById()`:** Retrieves a document by its ID.
  - **`save()`:** Saves a new document or updates an existing one

.

- **`remove()`:** Removes documents based on criteria.

**Usage Example:**

```javascript
const user = new User({ name: "John Doe" });
user.save().then(() => console.log("User saved"));
User.find({ name: "John Doe" }).then((users) => console.log(users));
```

**Explanation:**

- **Mongoose methods** simplify CRUD operations with MongoDB, providing a higher-level API to interact with database collections.

---

### **58. How do JWT and cookies work? What is the SHA-256 algorithm?**

**Explanation:**

**JWT** (JSON Web Token) and **cookies** are often used together for authentication:

- **JWT:** Used for stateless authentication. The server issues a token to the client, which the client sends back in subsequent requests.
- **Cookies:** Can store the JWT for client-side access. They are automatically sent with HTTP requests.

**SHA-256** is a cryptographic hash function that produces a 256-bit hash value, often used for securely hashing data.

**Usage Example for JWT in Cookies:**

```javascript
const jwt = require("jsonwebtoken");
const token = jwt.sign({ id: userId }, "secretKey", { algorithm: "HS256" });

// Set token in cookie
res.cookie("token", token, { httpOnly: true });
```

**Explanation:**

- **JWT** provides stateless authentication, while **cookies** help manage and store JWTs on the client side. **SHA-256** is used to ensure data integrity and security.

---

### **59. Why is fetching a token from the body less secure?**

**Explanation:**

Fetching a token from the **body** of a request is less secure due to:

- **Exposure:** Tokens in the body are accessible through JavaScript on the client-side, increasing the risk of exposure via XSS attacks.
- **Less Standard:** Using headers is a more common and standardized approach for token management.

**Usage Example:**

```javascript
// Less secure approach
fetch("https://api.example.com/data", {
  method: "POST",
  body: JSON.stringify({ token: "yourToken" }),
});
```

**Explanation:**

- **Fetching tokens from the body** introduces security risks, making it less favorable compared to using HTTP headers for token management.

---

### **60. What is cookie hijacking and token hijacking?**

**Explanation:**

- **Cookie Hijacking:** Refers to the theft of cookies from a user’s browser, potentially gaining unauthorized access to their session.
- **Token Hijacking:** Involves stealing authentication tokens, which can be used to impersonate the user or access restricted resources.

**Mitigation:**

- **Use Secure Flags:** For cookies, use `Secure` and `HttpOnly` flags.
- **Use HTTPS:** Ensure data is encrypted during transmission.

**Usage Example:**

```javascript
// Setting a secure cookie
res.cookie("token", "yourToken", { httpOnly: true, secure: true });
```

**Explanation:**

- **Cookie and token hijacking** are security risks that can be mitigated by using secure flags and encrypted connections.

---

### **61. What are pre and post middleware in backend development?**

**Explanation:**

**Pre Middleware:**

- **Purpose:** Executed before the main request handler. Used for tasks like authentication, logging, or validation.

**Post Middleware:**

- **Purpose:** Executed after the main request handler. Used for tasks like response formatting or cleanup.

**Usage Example:**

```javascript
const express = require("express");
const app = express();

// Pre middleware for logging
app.use((req, res, next) => {
  console.log("Request received");
  next();
});

// Main request handler
app.get("/", (req, res) => {
  res.send("Hello World");
});

// Post middleware for response modification
app.use((req, res, next) => {
  res.send("Response modified");
});

app.listen(3000);
```

**Explanation:**

- **Pre and post middleware** allow for flexible request handling and processing in backend applications, making it easier to manage different aspects of request and response life cycles.

---

### **62. What are AWS services like SQS and SNS?**

**Explanation:**

- **SQS (Simple Queue Service):**

  - **Purpose:** Provides a fully managed message queue service for storing and managing messages between distributed system components.
  - **Use Case:** Decoupling and scaling microservices.

- **SNS (Simple Notification Service):**
  - **Purpose:** Provides a fully managed publish/subscribe messaging service for sending notifications to subscribers.
  - **Use Case:** Sending alerts or notifications to multiple endpoints.

**Usage Example for SQS:**

```javascript
const AWS = require("aws-sdk");
const sqs = new AWS.SQS();

const params = {
  MessageBody: "Hello World",
  QueueUrl: "https://sqs.us-east-1.amazonaws.com/123456789012/MyQueue",
};

sqs.sendMessage(params, (err, data) => {
  if (err) console.log(err);
  else console.log(data);
});
```

**Explanation:**

- **SQS** and **SNS** are AWS services for managing messaging and notifications, helping in building scalable and reliable distributed systems.

---

### **63. What is a cron job?**

**Explanation:**

A **cron job** is a scheduled task that runs at specified intervals or times on a Unix-like operating system.

- **Usage Example:**

  - **Cron Syntax:** `* * * * * command` (minute, hour, day of month, month, day of week)

- **Example Cron Job:**
  ```bash
  # Run a script every day at midnight
  0 0 * * * /path/to/script.sh
  ```

**Explanation:**

- **Cron jobs** are used for automating repetitive tasks like backups, system maintenance, or scheduled reports.

---

### **64. What is a proxy server, and how does it work?**

**Explanation:**

A **proxy server** acts as an intermediary between a client and a destination server, handling requests and responses on behalf of the client.

- **Purpose:**
  - **Anonymity:** Hides the client’s IP address.
  - **Caching:** Stores frequently accessed data to improve performance.
  - **Filtering:** Blocks access to certain content or websites.

**Usage Example:**

```javascript
const http = require("http");
const httpProxy = require("http-proxy");

const proxy = httpProxy.createProxyServer({});

const server = http.createServer((req, res) => {
  proxy.web(req, res, { target: "http://example.com" });
});

server.listen(8000);
```

**Explanation:**

- **Proxy servers** enhance security, performance, and control over network traffic by managing requests and responses between clients and servers.

---

### **65. What is the difference between SHA (Secure Hashing Algorithm) and HMAC (Hashed-Based Message Authentication Code)?**

**Explanation:**

- **SHA (Secure Hashing Algorithm):**

  - **Purpose:** Produces a hash value from input data. It is used for data integrity checks.
  - **Example:** SHA-256 produces a 256-bit hash value.

- **HMAC (Hashed-Based Message Authentication Code):**
  - **Purpose:** Combines a hash function with a secret key to provide data integrity and authenticity.
  - **Example:** HMAC-SHA256 uses SHA-256 with a secret key.

**Usage Example for HMAC:**

```javascript
const crypto = require("crypto");
const secret = "mySecretKey";
const hash = crypto
  .createHmac("sha256", secret)
  .update("message")
  .digest("hex");
console.log(hash);
```

**Explanation:**

- **SHA** provides hash values for data integrity, while **HMAC** adds an additional layer of security by using a secret key to validate the authenticity of the data.

---

### **66. How does element matching and equality work in Mongoose?**

**Explanation:**

In **Mongoose**, element matching and equality queries are used to find documents based on specific criteria.

- **Equality Query:**

  - **Usage:** Matches documents where a field is equal to a specified value.
  - **Example:**
    ```javascript
    User.find({ name: "John Doe" }).then((users) => console.log(users));
    ```

- **Element Matching:**
  - **Usage:** Matches documents based on the presence or absence of elements.
  - **Example:**
    ```javascript
    User.find({ age: { $exists: true } }).then((users) => console.log(users));
    ```

**Explanation:**

- **Element matching** allows for flexible querying based on document structure, while **equality queries** help retrieve documents with specific field values.

---

### **67. What are aggregate methods in Mongoose?**

**Explanation:**

**Aggregate methods** in Mongoose are used to perform complex queries and data transformations, such as filtering, grouping, and sorting.

- **Common Methods:**
  - **`$match`:** Filters documents based on criteria.
  - **`$group`:** Groups documents by a specified field.
  - **`$sort`:** Sorts documents based on a field.

**Usage Example:**

```javascript
User.aggregate([
  { $match: { age: { $gte: 18 } } },
  { $group: { _id: "$city", count: { $sum: 1 } } },
  { $sort: { count: -1 } },
]).then((result) => console.log(result));
```

**Explanation:**

- **Aggregate methods** enable powerful data analysis and transformation capabilities in Mongoose, allowing for complex querying and reporting.

---

### \*\*68. What is

`const` and its usage in JavaScript?\*\*

**Explanation:**

**`const`** is a keyword used to declare variables whose values cannot be reassigned.

- **Usage:**
  - **Constant Values:** For values that should not change, such as configuration settings or fixed data.
  - **Block Scope:** Variables declared with `const` are block-scoped and cannot be redeclared within the same block.

**Usage Example:**

```javascript
const PI = 3.14;
PI = 3.1415; // Error: Assignment to constant variable
```

**Explanation:**

- **`const`** provides a way to create immutable variables, enhancing code reliability and preventing accidental changes to critical values.

---

### **69. What are JavaScript decorators, and how are they used?**

**Explanation:**

**Decorators** are a proposed JavaScript feature (currently at stage 2 in the TC39 process) that allows developers to modify classes and their members.

- **Usage:**
  - **Add Metadata:** Attach additional information to classes or methods.
  - **Modify Behavior:** Enhance or alter class methods and properties.

**Usage Example:**

```javascript
function readonly(target, key, descriptor) {
  descriptor.writable = false;
  return descriptor;
}

class Example {
  @readonly
  method() {
    console.log("This method cannot be modified");
  }
}
```

**Explanation:**

- **Decorators** provide a way to add metadata and modify class behavior in a declarative manner, though they are not yet a standard feature in JavaScript.

---

### **70. What are some common HTTP status codes and their meanings?**

**Explanation:**

**Common HTTP Status Codes:**

- **200 OK:** The request was successful.
- **201 Created:** The request was successful, and a new resource was created.
- **400 Bad Request:** The server could not understand the request due to invalid syntax.
- **401 Unauthorized:** Authentication is required and has failed or has not been provided.
- **404 Not Found:** The requested resource could not be found.
- **500 Internal Server Error:** The server encountered an error and could not complete the request.

**Usage Example:**

```javascript
res.status(404).send("Resource not found");
```

**Explanation:**

- **HTTP status codes** communicate the result of an HTTP request, helping clients understand the outcome and take appropriate actions.

---

### **71. What is the purpose of API versioning, and what methods are commonly used?**

**Explanation:**

**API Versioning** ensures backward compatibility and allows for incremental improvements without breaking existing clients.

- **Common Methods:**
  - **URL Path Versioning:** Including the version number in the URL path (e.g., `/api/v1/resource`).
  - **Query Parameter Versioning:** Using a query parameter to specify the version (e.g., `/api/resource?version=1`).
  - **Header Versioning:** Specifying the version in request headers (e.g., `Accept: application/vnd.example.v1+json`).

**Usage Example (URL Path Versioning):**

```javascript
app.use("/api/v1/resource", v1ResourceRouter);
app.use("/api/v2/resource", v2ResourceRouter);
```

**Explanation:**

- **API versioning** helps manage changes and updates in APIs, ensuring smooth transitions and compatibility for clients.

---

### **72. How do promises work in JavaScript?**

**Explanation:**

**Promises** are objects representing the eventual completion (or failure) of an asynchronous operation.

- **States:**

  - **Pending:** Initial state, neither fulfilled nor rejected.
  - **Fulfilled:** The operation completed successfully.
  - **Rejected:** The operation failed.

- **Usage:**
  - **`then()`:** Adds callbacks for when the promise is fulfilled or rejected.
  - **`catch()`:** Adds a callback for handling errors.

**Usage Example:**

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Success!"), 1000);
});

promise
  .then((result) => console.log(result))
  .catch((error) => console.error(error));
```

**Explanation:**

- **Promises** simplify handling asynchronous operations by providing a way to chain callbacks and manage errors effectively.

---

### **73. What are the differences between synchronous and asynchronous programming?**

**Explanation:**

- **Synchronous Programming:**

  - **Characteristics:** Operations are executed sequentially, blocking subsequent operations until the current one completes.
  - **Usage:** Simple scenarios where operations depend on each other and timing is crucial.

- **Asynchronous Programming:**
  - **Characteristics:** Operations can be executed independently, allowing other operations to proceed without waiting for the current one to complete.
  - **Usage:** Scenarios involving I/O operations, network requests, or tasks that may take an unpredictable amount of time.

**Usage Example:**

```javascript
// Synchronous
console.log("Start");
console.log("End");

// Asynchronous
console.log("Start");
setTimeout(() => console.log("Middle"), 1000);
console.log("End");
```

**Explanation:**

- **Synchronous programming** is simpler but can be inefficient, while **asynchronous programming** provides better performance and responsiveness for tasks that involve waiting or delays.

---

### **74. What is the difference between `null` and `undefined` in JavaScript?**

**Explanation:**

- **`null`:** Represents the intentional absence of any object value. It is often used to initialize variables with no value.

- **`undefined`:** Indicates that a variable has been declared but has not been assigned a value. It is also the default return value of functions that do not explicitly return anything.

**Usage Example:**

```javascript
let a = null;
let b;

console.log(a); // Outputs: null
console.log(b); // Outputs: undefined
```

**Explanation:**

- **`null`** and **`undefined`** are distinct values in JavaScript, with **`null`** representing a deliberate lack of value and **`undefined`** indicating that a variable has not been initialized.

---

### **75. What is the difference between `==` and `===` in JavaScript?**

**Explanation:**

- **`==` (Loose Equality):** Compares values for equality after performing type coercion. It converts the operands to the same type before comparison.

- **`===` (Strict Equality):** Compares values for equality without type coercion. It returns true only if both the value and the type are the same.

**Usage Example:**

```javascript
console.log(5 == "5"); // Outputs: true (type coercion occurs)
console.log(5 === "5"); // Outputs: false (different types)
```

**Explanation:**

- **`==`** allows type coercion, which can lead to unexpected results, while **`===`** ensures that both value and type are considered in comparisons, leading to more predictable and reliable code.

---

### **76. How does the `fetch` API work in JavaScript?**

**Explanation:**

The **`fetch` API** is used to make network requests in JavaScript, providing a more modern and flexible alternative to `XMLHttpRequest`.

- **Usage:**
  - **Making Requests:** `fetch()` returns a promise that resolves to the response of the request.
  - **Handling Responses:** You can use `.then()` to handle the response and parse it as needed.

**Usage Example:**

```javascript
fetch("https://api.example.com/data")
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

**Explanation:**

- **`fetch`** simplifies network requests by providing a promise-based interface and allowing easy handling of responses and errors.

---

### **77. What is the purpose of the `this` keyword in JavaScript?**

**Explanation:**

The **`this`** keyword refers to the context in which a function or method is executed. Its value depends on how the function is called.

- **Global Context:** In the global execution context, `this` refers to the global object (e.g., `window` in browsers).
- **Object Methods:** In methods, `this` refers to the object the method is called on.
- **Constructor Functions:** In constructors, `this` refers to the newly created instance.

**Usage Example:**

```javascript
const person = {
  name: "Alice",
  greet: function () {
    console.log("Hello, " + this.name);
  },
};

person.greet(); // Outputs: Hello, Alice
```

**Explanation:**

- **`this`** provides context-specific access to properties and methods, enabling dynamic behavior based on the execution context.

---

### **78. How does event delegation work in JavaScript?**

**Explanation:**

**Event delegation** involves attaching a single event listener to a parent element that handles events for multiple child elements. This technique leverages event bubbling to manage events efficiently.

- **Advantages:**
  - **Performance:** Reduces the number of event listeners, improving performance.
  - **Dynamic Content:** Handles events for dynamically added elements.

**Usage Example:**

```javascript
document.getElementById("parent").addEventListener("click", function (event) {
  if (event.target && event.target.matches("button.child")) {
    console.log("Child button clicked");
  }
});
```

**Explanation:**

- **Event delegation** improves performance and flexibility by using a single event listener on a parent element to manage events for its child elements.

---

### **79. What are the differences between `localStorage` and `sessionStorage`?**

**Explanation:**

- **`localStorage`:** Stores data with no expiration time

. Data persists even after the browser is closed and reopened.

- **`sessionStorage`:** Stores data for the duration of the page session. Data is cleared when the page session ends (e.g., when the tab or browser is closed).

**Usage Example:**

```javascript
// localStorage
localStorage.setItem("key", "value");
console.log(localStorage.getItem("key")); // Outputs: value

// sessionStorage
sessionStorage.setItem("key", "value");
console.log(sessionStorage.getItem("key")); // Outputs: value
```

**Explanation:**

- **`localStorage`** is used for long-term storage, while **`sessionStorage`** is for temporary storage that is cleared with the session.

---

### **80. How do async/await work in JavaScript?**

**Explanation:**

**`async/await`** are used for handling asynchronous operations in a more readable and synchronous-like manner.

- **`async` Function:** Declares a function as asynchronous, allowing the use of `await` inside it.
- **`await` Expression:** Pauses the execution of the `async` function until the promise is resolved.

**Usage Example:**

```javascript
async function fetchData() {
  try {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Error:", error);
  }
}

fetchData();
```

**Explanation:**

- **`async/await`** simplifies handling asynchronous code, making it easier to read and maintain compared to traditional promise chaining.

---

### **81. What is the purpose of the `constructor` method in a class in JavaScript?**

**Explanation:**

The **`constructor`** method is a special method for creating and initializing objects created within a class.

- **Usage:** It is called when a new instance of the class is created, allowing for setting up initial properties and performing setup operations.

**Usage Example:**

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
}

const person = new Person("John");
console.log(person.name); // Outputs: John
```

**Explanation:**

- The **`constructor`** method initializes new objects and sets up necessary properties, ensuring proper object creation.

---

### **82. How do JavaScript modules work?**

**Explanation:**

**JavaScript modules** allow code to be divided into smaller, reusable pieces. Modules can export functionality and import it into other modules.

- **`export` Statement:** Exposes functions, objects, or values to other modules.
- **`import` Statement:** Imports functionality from other modules.

**Usage Example:**

```javascript
// module.js
export const greet = (name) => `Hello, ${name}`;

// main.js
import { greet } from "./module.js";
console.log(greet("Alice")); // Outputs: Hello, Alice
```

**Explanation:**

- **JavaScript modules** enable better code organization and reuse, promoting maintainability and scalability in applications.

---

### **83. What is the `spread` operator and its uses in JavaScript?**

**Explanation:**

The **`spread` operator** (`...`) is used to expand or spread elements of an iterable (e.g., array) into individual elements.

- **Usage Examples:**
  - **Arrays:** Copying and merging arrays.
  - **Function Calls:** Passing arguments to functions.

**Usage Example:**

```javascript
const numbers = [1, 2, 3];
const moreNumbers = [...numbers, 4, 5];
console.log(moreNumbers); // Outputs: [1, 2, 3, 4, 5]

const add = (a, b, c) => a + b + c;
const args = [1, 2, 3];
console.log(add(...args)); // Outputs: 6
```

**Explanation:**

- The **`spread` operator** simplifies working with arrays and function arguments by expanding iterables into individual elements.

---

### **84. What are arrow functions, and how do they differ from regular functions?**

**Explanation:**

**Arrow functions** provide a more concise syntax for writing functions and have different behavior for the `this` keyword.

- **Syntax:**

  ```javascript
  const add = (a, b) => a + b;
  ```

- **Differences from Regular Functions:**
  - **No `this` Binding:** Arrow functions do not have their own `this`; they inherit it from the surrounding context.
  - **No `arguments` Object:** Arrow functions do not have their own `arguments` object.

**Usage Example:**

```javascript
const obj = {
  value: 10,
  getValue: function () {
    return (() => this.value)();
  },
};

console.log(obj.getValue()); // Outputs: 10
```

**Explanation:**

- **Arrow functions** offer a more concise syntax and different behavior for `this`, making them useful for specific contexts and situations.

---

### **85. How do `map` and `filter` methods work in JavaScript?**

**Explanation:**

- **`map`:** Creates a new array with the results of calling a provided function on every element in the calling array.

**Usage Example:**

```javascript
const numbers = [1, 2, 3];
const doubled = numbers.map((x) => x * 2);
console.log(doubled); // Outputs: [2, 4, 6]
```

- **`filter`:** Creates a new array with all elements that pass the test implemented by the provided function.

**Usage Example:**

```javascript
const numbers = [1, 2, 3];
const even = numbers.filter((x) => x % 2 === 0);
console.log(even); // Outputs: [2]
```

**Explanation:**

- **`map`** and **`filter`** methods provide powerful ways to transform and filter arrays, enabling more functional programming techniques in JavaScript.

---

### **86. What is the purpose of `async` and `await` in JavaScript?**

**Explanation:**

**`async` and `await`** are used for handling asynchronous operations more intuitively and synchronously.

- **`async` Function:** Declares a function as asynchronous, enabling the use of `await` within it.
- **`await` Expression:** Pauses the execution of the `async` function until the promise is resolved.

**Usage Example:**

```javascript
async function fetchData() {
  try {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Error:", error);
  }
}

fetchData();
```

**Explanation:**

- **`async` and `await`** simplify the process of working with asynchronous operations, making the code more readable and easier to manage compared to traditional promise chaining.

---

### **87. How does event delegation improve performance in web applications?**

**Explanation:**

**Event delegation** improves performance by:

- **Reducing the Number of Event Listeners:** Attaches a single event listener to a parent element instead of multiple listeners to individual child elements.
- **Handling Dynamic Content:** Works for dynamically added elements without needing to attach new event listeners.

**Usage Example:**

```javascript
document.getElementById("parent").addEventListener("click", function (event) {
  if (event.target && event.target.matches("button.child")) {
    console.log("Child button clicked");
  }
});
```

**Explanation:**

- **Event delegation** reduces overhead and improves performance by managing events efficiently and accommodating dynamically changing content.

---

### **88. What are the benefits and limitations of using `localStorage` in web applications?**

**Explanation:**

**Benefits of `localStorage`:**

- **Persistent Storage:** Data persists even after the browser is closed.
- **Simple API:** Easy to use with a straightforward key-value storage mechanism.

**Limitations of `localStorage`:**

- **Size Limitation:** Typically limited to around 5-10MB per origin.
- **No Expiry:** Data does not automatically expire, which might lead to outdated or stale data.
- **Security Concerns:** Data stored in `localStorage` is accessible through JavaScript and can be vulnerable to XSS attacks.

**Usage Example:**

```javascript
localStorage.setItem("key", "value");
console.log(localStorage.getItem("key")); // Outputs: value
```

**Explanation:**

- **`localStorage`** is useful for persistent storage but comes with limitations and security considerations that should be taken into account.

---

### **89. What are some common methods for handling asynchronous operations in JavaScript?**

**Explanation:**

Common methods for handling asynchronous operations include:

- **Callbacks:** Functions passed as arguments to be executed after the asynchronous operation completes.
- **Promises:** Objects representing the eventual completion or failure of an asynchronous operation.
- **Async/Await:** Syntax for handling promises in a more synchronous-like manner.

**Usage Example (Promise):**

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Success!"), 1000);
});
promise.then((result) => console.log(result));
```

**Usage Example (Async/Await):**

```javascript
async function fetchData() {
  const response = await fetch("https://api.example.com/data");
  const data = await response.json();
  console.log(data);
}
fetchData();
```

**Explanation:**

- **Callbacks**, **promises**, and **async/await** are common methods for managing asynchronous operations, each with its own advantages and use cases.

---

### \*\*90. What is the purpose

of `Object.freeze` in JavaScript?\*\*

**Explanation:**

**`Object.freeze`** is a method used to freeze an object, preventing modifications to its properties and making it immutable.

- **Usage:**
  - **Prevent Modifications:** Prevent changes to existing properties and disallow adding or removing properties.
  - **Deep Freeze:** For deep immutability, additional recursive freezing is required.

**Usage Example:**

```javascript
const obj = { name: "Alice" };
Object.freeze(obj);
obj.name = "Bob"; // No effect
console.log(obj.name); // Outputs: Alice
```

**Explanation:**

- **`Object.freeze`** ensures that objects cannot be altered, which can be useful for enforcing immutability and preventing unintended changes.

---

### **91. What is the `new` keyword used for in JavaScript?**

**Explanation:**

The **`new`** keyword is used to create instances of user-defined objects or built-in objects that have a constructor function.

- **Usage:**
  - **Create Instances:** Instantiate new objects with a constructor.
  - **Set Up Context:** Automatically sets the context (`this`) within the constructor function.

**Usage Example:**

```javascript
function Person(name) {
  this.name = name;
}

const person = new Person("Alice");
console.log(person.name); // Outputs: Alice
```

**Explanation:**

- **`new`** initializes new instances and sets up the context for constructors, enabling object creation and initialization.

---

### **92. How do `try...catch` blocks work in JavaScript?**

**Explanation:**

**`try...catch`** blocks are used to handle exceptions and errors that occur during the execution of code.

- **`try` Block:** Contains code that may throw an error.
- **`catch` Block:** Contains code that handles the error if one occurs.

**Usage Example:**

```javascript
try {
  let result = riskyFunction();
} catch (error) {
  console.error("An error occurred:", error);
}
```

**Explanation:**

- **`try...catch`** provides a way to handle errors gracefully, allowing the program to continue running even if an error occurs.

---

### **93. What is the `prototype` property in JavaScript?**

**Explanation:**

The **`prototype`** property allows for the inheritance of properties and methods from one object to another.

- **Usage:**
  - **Add Methods:** Add methods to constructor functions or classes.
  - **Inheritance:** Enable object inheritance and method sharing.

**Usage Example:**

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function () {
  return `Hello, ${this.name}`;
};

const person = new Person("Alice");
console.log(person.greet()); // Outputs: Hello, Alice
```

**Explanation:**

- The **`prototype`** property provides a mechanism for defining and sharing methods across instances, enabling inheritance and code reuse.

---

### **94. What is the `this` context in arrow functions?**

**Explanation:**

In **arrow functions**, **`this`** does not have its own context; instead, it inherits the `this` value from the surrounding lexical context.

- **Usage:**
  - **Inherit `this`:** Useful in scenarios where `this` needs to refer to the surrounding context.

**Usage Example:**

```javascript
function Timer() {
  this.seconds = 0;
  setInterval(() => {
    this.seconds++;
    console.log(this.seconds);
  }, 1000);
}

const timer = new Timer();
```

**Explanation:**

- **Arrow functions** inherit `this` from their enclosing scope, avoiding issues with `this` binding in traditional functions.

---

### **95. What is the purpose of `Object.assign` in JavaScript?**

**Explanation:**

**`Object.assign`** is used to copy the values of all enumerable properties from one or more source objects to a target object.

- **Usage:**
  - **Merge Objects:** Combine multiple objects into one.
  - **Clone Objects:** Create a shallow copy of an object.

**Usage Example:**

```javascript
const target = { a: 1 };
const source = { b: 2 };

Object.assign(target, source);
console.log(target); // Outputs: { a: 1, b: 2 }
```

**Explanation:**

- **`Object.assign`** simplifies object manipulation by providing a straightforward way to copy and merge properties.

---

### **96. What is the purpose of the `bind` method in JavaScript?**

**Explanation:**

The **`bind`** method creates a new function with a specific `this` value and, optionally, pre-set arguments.

- **Usage:**
  - **Set `this`:** Bind a specific context to a function.
  - **Partial Application:** Pre-set arguments for function invocation.

**Usage Example:**

```javascript
function greet() {
  console.log(`Hello, ${this.name}`);
}

const person = { name: "Alice" };
const boundGreet = greet.bind(person);
boundGreet(); // Outputs: Hello, Alice
```

**Explanation:**

- **`bind`** provides control over the `this` context and function arguments, making it useful for customizing function behavior and context.

---

### **97. How does the `for...of` loop work in JavaScript?**

**Explanation:**

The **`for...of`** loop iterates over iterable objects, such as arrays, strings, and maps, returning the values of each element.

- **Usage:**
  - **Iterate Values:** Access the values of an iterable directly.
  - **Avoid Index:** Simplifies iteration without dealing with indexes.

**Usage Example:**

```javascript
const numbers = [1, 2, 3];
for (const number of numbers) {
  console.log(number);
}
// Outputs: 1, 2, 3
```

**Explanation:**

- **`for...of`** provides a straightforward way to iterate over values in an iterable, making the code cleaner and easier to understand.

---

### **98. What are template literals, and how are they used in JavaScript?**

**Explanation:**

**Template literals** are a feature in JavaScript that allows for multi-line strings and embedded expressions.

- **Syntax:**
  - **Backticks (`):** Use backticks to define template literals.
  - **Embedded Expressions:** Use `${expression}` to embed expressions within the string.

**Usage Example:**

```javascript
const name = "Alice";
const message = `Hello, ${name}!`;
console.log(message); // Outputs: Hello, Alice!
```

**Explanation:**

- **Template literals** provide a flexible and readable way to handle strings, including multi-line text and embedded expressions.

---

### **99. How does the `default` keyword work in JavaScript functions?**

**Explanation:**

The **`default`** keyword allows setting default values for function parameters when no value is provided.

- **Usage:**
  - **Provide Defaults:** Define default values for parameters in function declarations.

**Usage Example:**

```javascript
function greet(name = "Guest") {
  console.log(`Hello, ${name}`);
}

greet(); // Outputs: Hello, Guest
greet("Alice"); // Outputs: Hello, Alice
```

**Explanation:**

- **`default`** values simplify function calls by providing fallback values when arguments are not passed.

---

### **100. What is the purpose of the `Symbol` type in JavaScript?**

**Explanation:**

**`Symbol`** is a primitive data type used to create unique identifiers for object properties.

- **Usage:**
  - **Unique Keys:** Create unique property keys to avoid collisions.
  - **Well-Known Symbols:** Access built-in symbols for specific behavior (e.g., `Symbol.iterator`).

**Usage Example:**

```javascript
const uniqueId = Symbol("id");
const obj = { [uniqueId]: 123 };

console.log(obj[uniqueId]); // Outputs: 123
```

**Explanation:**

- **`Symbol`** provides a way to create unique property keys, ensuring that property names do not conflict and are used for special cases.
