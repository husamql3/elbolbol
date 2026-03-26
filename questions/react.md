# React

<!-- markdownlint-disable MD033 -->

<details>
<summary>What is React? Describe the benefits of React</summary>

React is an open-source JavaScript library developed by Facebook for building user interfaces. It focuses on the view layer of an application and is especially useful for creating single-page applications where a seamless user experience is crucial.

1. Component-based architecture: Modular and reusable, Maintainable**,** Easier to test
2. Virtual DOM and efficient updates
3. Large and active community
4. Learn once, write anywhere: Share code between platforms (react native)

</details>

<details>
<summary>What is the difference between <code>state</code> and <code>props</code> in React?</summary>

- State is managed within the component, while props are passed from the parent
- State can change over time, while props are immutable
- State is used for data that changes within a component, while props are used to pass data and event handlers to child components

</details>

<details>
<summary>What is the purpose of the <code>key</code> prop in React?</summary>

The **`key`** prop is a special attribute you need to include when creating lists of elements in React. It is crucial for helping React identify which items have changed, been added, or removed, thereby optimizing the rendering process.

Why `key` is important **→** Efficient updates, Avoiding bugs, and Performance optimization

</details>

<details>
<summary>What are the benefits of using hooks in React?</summary>

- **Simplified state management:** Hooks like **`useState`** allow you to add state to functional components without converting them to class components.
- **Improved code readability:** Hooks help in breaking down complex components into smaller, reusable pieces of logic.
- **Reusable logic:** Custom hooks allow you to extract and reuse stateful logic across multiple components. This promotes code reuse and reduces duplication.
- **Reduced need for lifecycle methods:** Hooks like **`useEffect`** can replace lifecycle methods such as **`componentDidMount`**, **`componentDidUpdate`**, and **`componentWillUnmount`**. This simplifies the component lifecycle management.
- **Better separation of concerns:** Hooks allow you to separate concerns by grouping related logic together. This makes the codebase more maintainable and easier to debug.

</details>

<details>
<summary>What are the rules of React hooks?</summary>

- Always call hooks at the top level
- Only call hooks from React function components or custom hooks

</details>

<details>
<summary>What does re-rendering mean in React?</summary>

- **Understanding re-rendering:** Re-rendering in React is the process by which a component updates its output to the DOM in response to changes in its state or props. This ensures that the UI is always in sync with the underlying data.
- Re-rendering occurs in the following scenarios:
  - When a component's state changes using **`setState`**
  - When a component receives new props from its parent component
  - When the parent component re-renders, causing its child components to re-render as well
- **The re-rendering process**
  1. **State or props change**: When a component's state or props change, React schedules a re-render for that component.
  2. **Render method**: React calls the component's **`render`** method to generate a new virtual DOM tree.
  3. **Virtual DOM comparison**: React compares the new virtual DOM tree with the previous one using a diffing algorithm.
  4. **DOM updates**: React calculates the minimal set of changes required and updates the actual DOM accordingly.

</details>

<details>
<summary>Explain the difference between <code>useMemo</code> and <code>useCallback</code>?</summary>

Both are React hooks for **memoization,** they cache a value to avoid expensive recalculations on every render. The key difference is _what_ they memoize.

- `useMemo` — memoizes a **computed value**
  - Use it when you want to avoid re-running an expensive calculation
  - Returns the **result** of calling the function
- `useCallback` — memoizes a **function reference**
  - Use it when you want to keep a function's reference stable across renders, typically to prevent child components from re-rendering unnecessarily.
  - Returns the **function itself**

</details>

<details>
<summary>How would one optimize the performance of React contexts to reduce re-renders?</summary>

- **Memoizing context values:** One of the most effective ways to reduce unnecessary rerenders is to memoize the context value. By using **`useMemo`**, you can ensure that the context value only changes when its dependencies change.
- **Splitting contexts:** Another technique is to split your context into multiple smaller contexts. This way, you can isolate state changes to specific parts of your application, reducing the number of components that need to re-render.
- **Using selectors:** Using selectors can help you only re-render components that actually need the updated context value.

</details>

<details>
<summary>How do you handle asynchronous data loading in React applications?</summary>

- **Using `useEffect` and `useState`**
  - **Initialize state** → \*\*\*\*`const [data, setData] = useState(null);`
  - **Fetch data** → using `useEffect` when the component mounts
  - **Update state** → `setData(result);`
- **Handling errors:** It's important to handle errors that may occur during data fetching. You can use a **`try-catch`** block within the **`useEffect`** to catch and handle errors.
- **Using custom hooks:** For better code reusability, you can create custom hooks to handle data fetching. This allows you to encapsulate the data fetching logic and reuse it across multiple components.

```javascript
function useFetch(url) {
  // fetching
  return { data, loading, error };
}
```

</details>

<details>
<summary>How do you decide between using <code>state</code>, <code>context</code>, and <code>external state managers</code>?</summary>

- **React state:** React state is best suited for managing local state within a single component. It is simple to use and provides a straightforward way to handle state that does not need to be shared across multiple components.
  - When the state is only relevant to a single component
  - When the state does not need to be accessed or modified by other components
  - When you want to keep the component self-contained and easy to understand
- **React context:** React context is useful for sharing state across multiple components without having to pass props down through every level of the component tree. It is ideal for global state that needs to be accessed by many components.
  - When you need to share state across multiple components
  - When you want to avoid prop drilling
  - When the state is relatively simple and does not require advanced state management features
- **External state managers:** External state managers like Redux or MobX are designed for complex state management needs. Providing advanced features such as middleware, time-travel debugging, and the ability to manage state across a large application.
  - When the state management needs are complex and involve many interconnected pieces of state
  - When you need advanced features like middleware, time-travel debugging
  - When the state needs to be shared across a large application with many components

</details>

<details>
<summary>What is virtual DOM in React?</summary>

- The virtual DOM in React is a lightweight copy of the actual DOM. It allows React to efficiently update the UI by comparing the virtual DOM with the real DOM and only making necessary changes.
  1. **Initial rendering**: When a React component is rendered for the first time, a virtual DOM tree is created. This tree is a lightweight copy of the actual DOM.
  2. **Updating state**: When the state of a component changes, a new virtual DOM tree is created. React then compares this new tree with the previous one.
  3. **Diffing algorithm**: React uses a diffing algorithm to find the differences between the new virtual DOM tree and the previous one. This process is called reconciliation.
  4. **Updating the real DOM (Reconciliation)**: React updates only the parts of the real DOM that have changed, rather than re-rendering the entire UI.

</details>

<details>
<summary>What is the difference between <code>useEffect</code> and <code>useLayoutEffect</code>?</summary>

- `useEffect` — after paint (async)

```javascript
useEffect(() => {
  fetchData(); // runs after user sees the new UI
}, [id]);
```

- `useLayoutEffect` — before paint (synchronous)

```javascript
useLayoutEffect(() => {
  const height = ref.current.getBoundingClientRect().height;
  setTooltipPosition(height); // runs before user sees anything
}, []);
```

</details>

<details>
<summary>What is <code>React Fiber</code> and how is it an improvement over the previous approach?</summary>

React Fiber is a re-implementation of React's core algorithm for rendering and reconciliation. It was introduced in React 16 to address limitations in the previous stack-based algorithm

- **Incremental rendering**
  The previous stack-based algorithm processed updates in a single, synchronous pass, which could lead to performance issues, especially with complex UIs.
- **Time slicing**
  React Fiber introduces the concept of time slicing, which allows React to prioritize updates based on their urgency.
- **Concurrency**
  With Fiber, React can work on multiple tasks concurrently. This means that React can start rendering updates while still processing other tasks, leading to a smoother and more responsive user experience.

  > rendering was **synchronous and uninterruptible** — once React started rendering a tree, it blocked the main thread until it finished. Concurrent React makes rendering **interruptible** — React can pause work, prioritize urgent updates, and resume later.

- **Error boundaries**
  React Fiber introduced error boundaries, which allow developers to catch and handle errors in the component tree gracefully. This was not possible with the previous stack-based algorithm, where errors could cause the entire application to crash.
- **Improved support for animations**
  Fiber's incremental rendering and time slicing capabilities make it easier to implement smooth animations and transitions. React can now prioritize animation frames and ensure that they are rendered in a timely manner, leading to a better user experience.

</details>

<details>
<summary>What is the <code>useRef</code> hook and what are its common use cases?</summary>

The `useRef` hook creates a mutable object that persists across renders without causing re-renders. It is commonly used to access DOM elements or store mutable values.

</details>

<details>
<summary>What are higher order components (HOC) in React?</summary>

functions in React that take a component as an argument and return a new component. The new component typically wraps the original component and adds additional props, state, or behavior. HOCs are a pattern for reusing component logic.

- Share common functionality between components
- Abstract and reuse component logic
- Enhance components with additional props or state

|                      | **HOC**                                  | **Hooks**       |
| -------------------- | ---------------------------------------- | --------------- |
| **Boilerplate**      | High                                     | Low             |
| **Composability**    | Wrapper hell                             | Flat, linear    |
| **Props collision**  | ⚠️ Risk                                  | ❌ None         |
| **Debugging**        | Hard (nested tree)                       | Easy            |
| **Error boundaries** | ✅ Only option                           | ❌ Not possible |
| **Best for**         | Error boundaries, injecting JSX wrappers | Everything else |

> Hooks replaced HOCs for **logic reuse**. But HOCs still have a place for **structural wrapping,** injecting wrapper JSX, error boundaries, or decorating third-party components you don't control.

</details>

<details>
<summary>Composition over Inheritance in React</summary>

- **Inheritance:** In OOP, you'd extend a base class to share behavior
- **Composition:** Instead of extending, you **combine components** by passing them as props or children.
- **Pattern 1** — **`children` prop (containment)**
  When a component doesn't know its children ahead of time
- **Pattern 2** — \**\*\*Passing components as props (slots)
  For more control over *where\* things are placed:
- **Pattern 3** — Higher Order Components (HOC)
  Wrapping a component to inject behavior

</details>

<details>
<summary>Explain what React hydration is?</summary>

- **Hydration process:** the process that happens after the server-side rendered HTML is sent to the client. React takes the static HTML and "hydrates" it by attaching event listeners and initializing the state, making the page interactive. This process involves:
  1. **Reusing the existing HTML**: React uses the HTML generated by the server and does not re-render it from scratch.
  2. **Attaching event listeners**: React attaches the necessary event listeners to the existing HTML elements.
  3. **Initializing state**: React initializes the component state and props to make the page dynamic.
- **Server-side rendering (SSR)**
  a technique where the HTML of a web page is generated on the server and sent to the client. This allows for faster initial page loads and better SEO since the content is already available when the page is loaded.
- **Benefits of hydration:**
  1. **Faster initial load**: Since the HTML is already available, the initial page load is faster.
  2. **SEO benefits**: Search engines can crawl the server-rendered HTML, improving SEO.
  3. **Improved user experience**: Users can see the content immediately, even before React has fully taken over.
- **What is a Hydration Mismatch?**
  A mismatch happens when the HTML the **server rendered** doesn't match what **React tries to render on the client**. React expects them to be identical so it can efficiently attach to the existing DOM — if they differ, React has to throw away the server HTML and re-render from scratch, defeating the purpose of SSR.
  1. Using browser-only APIs during render
     window doesn't exist on the server
     `const width = window.innerWidth;`
  2. Dates and times
     Server and client render at different moments
     `<p>Rendered at: {new Date().toLocaleString()}</p>`
  3. Random values
     Different on every render
     `const id = Math.random();`
  4. User-specific data rendered immediately
     Server doesn't know if user is logged in
     `<p>Hello {user.name}</p>`
  5. useLayoutEffect
     Doesn't run on server, causes mismatch on client
     `useLayoutEffect(() => { ... }, []);`
- **How to Fix Mismatches**
  1. **Delay browser-only code with `useEffect`**

```javascript
useEffect(() => {
  setWidth(window.innerWidth); // runs only on client
}, []);
```

2. `suppressHydrationWarning` for intentional differences

```javascript
// For timestamps or truly unavoidable differences
<time suppressHydrationWarning>{new Date().toLocaleString()}</time>
```

3. Mount guard pattern

```javascript
const [mounted, setMounted] = useState(false);

useEffect(() => setMounted(true), []);

if (!mounted) return null; // render nothing on server
return <ComponentThatNeedsBrowser />;
```

</details>

<details>
<summary><code>Next.js</code> rendering modes — <code>SSR</code>, <code>SSG</code>, <code>ISR</code>, <code>RSC</code></summary>

1. **Client-Side Rendering (CSR):** The original React model. Server sends a bare HTML shell, browser downloads JS, React builds the DOM entirely on the client.
   `Server → empty <div id="root">`
   `Client → downloads JS → React renders → fetches data → renders again`
   **Good for:** Dashboards, admin panels, anything behind a login where SEO doesn't matter.
   **Bad for:** SEO, initial load performance (user sees blank screen while JS loads).
2. **Static Site Generation (SSG):** HTML is generated **at build time**. The same HTML file is served to every user. Fastest possible delivery, can be served from a CDN.
   `Build time → generates HTML files`
   `Request    → CDN serves pre-built HTML instantly`
   **Good for:** Marketing pages, blogs, docs — content that doesn't change per user or per request.
   **Bad for:** Personalized content, frequently changing data.
3. **Server-Side Rendering (SSR):** HTML is generated **on every request** on the server. Fresh data every time, but slower than SSG since there's no caching.
   `Request → server fetches data → generates HTML → sends to client`
   **Good for:** Pages that need fresh data and SEO — e.g. a product page with live inventory
   **Bad for:** High traffic pages where per-request cost adds up
4. **Incremental Static Regeneration (ISR):** Pages are statically generated but **revalidated in the background** after a time window. Best of both SSG and SSR.
   `Build time  → generates HTML`
   `Request 1   → serves cached HTML`
   `Request 2   → serves cached HTML, triggers background regeneration`
   `Request 3   → serves newly regenerated HTML`
   **Good for:** E-commerce product pages, news articles, content that changes but not on every request
   **Bad for:** Data that must be real-time accurate
5. **React Server Components (RSC):** Components themselves are split into **server** and **client,** server components run only on the server and never ship their JS to the browser.
   `Server components → rendered on server, zero JS bundle cost`
   `Client components → hydrated on client, interactive`
6. **Streaming SSR:** Instead of waiting for the entire page to render before sending HTML, React streams it in **chunks** as each piece becomes ready. Uses React's `Suspense` as the boundary
   `Request → server streams Header + Footer immediately`
   `        → SlowDataComponent streams in when its data resolves`
   `        → user sees progressive content instead of blank screen`

| Strategy      | Where rendered | When                  | SEO | Fresh data | Speed        |
| ------------- | -------------- | --------------------- | --- | ---------- | ------------ |
| **CSR**       | Client         | Runtime               | ❌  | ✅         | Slow initial |
| **SSG**       | Server         | Build time            | ✅  | ❌         | Fastest      |
| **SSR**       | Server         | Per request           | ✅  | ✅         | Medium       |
| **ISR**       | Server         | Build + revalidate    | ✅  | ✅         | Fast         |
| **RSC**       | Server         | Per request           | ✅  | ✅         | Small bundle |
| **Streaming** | Server         | Per request (chunked) | ✅  | ✅         | Progressive  |

</details>

<details>
<summary><code>Next.js</code> FAQ Page Patterns — When to Use Which Rendering Mode?</summary>

The decision tree comes down to three questions: **Does it need SEO? Does data change? Is it personalized?**

```
Is content personalized per user?
├── YES → SSR or CSR (behind auth)
└── NO
    ├── Does data change frequently?
    │   ├── YES, real-time → SSR + Streaming
    │   ├── YES, occasionally → ISR
    │   └── NO → SSG
    └── Does it need SEO?
        ├── YES → SSG / SSR / ISR
        └── NO → CSR
```

</details>

<details>
<summary><code>useRef</code> and <code>forwardRef</code> — DOM access, imperative handles</summary>

- `useRef` - two distinct use cases, The key insight: **`useRef` returns the same object every render.** Mutating `.current` doesn't cause a re-render — unlike `useState`.
  - Use case 1: DOM access

```javascript
function TextInput() {
  const inputRef = useRef(null);

  function focusInput() {
    inputRef.current.focus(); // direct DOM manipulation
  }

  return (
    <>
      <input ref={inputRef} />
      <button onClick={focusInput}>Focus</button>
    </>
  );
}
```

- Use case 2: Persisting values across renders without triggering re-render

```javascript
function Timer() {
  const intervalRef = useRef(null);

  function start() {
    intervalRef.current = setInterval(() => console.log("tick"), 1000);
  }

  function stop() {
    clearInterval(intervalRef.current); // stable reference, no re-render
  }
}
```

- `forwardRef` — passing refs to child components, By default, you can't pass a `ref` to a custom component — refs aren't props. `forwardRef` lets a parent reach into a child's DOM.
- In React 19, `ref` is now a regular prop, so `forwardRef` is no longer needed

</details>

<details>
<summary><code>Redux</code> vs <code>Zustand</code> vs <code>Context API</code></summary>

|                   | Context API                      | Redux                      | Zustand          |
| ----------------- | -------------------------------- | -------------------------- | ---------------- |
| Bundle size       | Zero                             | ~50kb                      | ~1kb             |
| Boilerplate       | Low                              | High                       | Very low         |
| Re-render control | ❌ Poor                          | ✅ Selectors               | ✅ Selectors     |
| DevTools          | ❌ None                          | ✅ Excellent               | ✅ Good          |
| Learning curve    | None                             | Steep                      | Minimal          |
| Best for          | Infrequent updates (theme, auth) | Large teams, complex state | Most modern apps |

</details>

<details>
<summary>Data Fetching Patterns</summary>

|                   | **useEffect**   | **React Query**      | **SWR**            | **RSC**            |
| ----------------- | --------------- | -------------------- | ------------------ | ------------------ |
| **Caching**       | ❌ Manual       | ✅ Built-in          | ✅ Built-in        | ✅ Server-side     |
| **Deduplication** | ❌              | ✅                   | ✅                 | ✅                 |
| **Bundle cost**   | Zero            | ~13kb                | ~4kb               | Zero               |
| **Real-time**     | Manual          | ✅ Polling/WS        | ✅ Polling         | ❌                 |
| **Best for**      | Simple one-offs | Complex client state | Lightweight client | Next.js App Router |

</details>

<details>
<summary>Implementing a Design System That Scales Across Teams</summary>

1. Design Tokens (the foundation): Tokens are the single source of truth for all visual decisions. Everything else derives from them.

```javascript
// tokens.js — platform-agnostic, can generate CSS, iOS, Android
export const tokens = {
  color: {
    brand: {
      primary: '#0066FF',
      primaryHover: '#0052CC',
...
```

2. Primitive Components: Unstyled or minimally styled, maximally composable. These are the atoms.
   **The key rule:** primitives should be flexible enough that teams **never need to fork them**. Every reasonable variant should be a prop.
3. Compound Components (composition pattern)**:** For complex components, expose a composable API rather than a monolithic prop surface

```javascript
// ❌ Monolithic — props explosion, hard to extend
<Card
  title="Hello"
  subtitle="World"
  image="/img.jpg"
  actions={[...]}
  footerText="..."
/>

// ✅ Compound — composable, flexible, readable
<Card>
  <Card.Image src="/img.jpg" alt="..." />
  <Card.Body>
    <Card.Title>Hello</Card.Title>
    <Card.Subtitle>World</Card.Subtitle>
  </Card.Body>
  <Card.Footer>
    <Button>Action</Button>
  </Card.Footer>
</Card>
```

4. Versioning and change management: Patch, Minor, Major
5. Documentation and governance

</details>

<details>
<summary>What is <code>react-helmet</code>?</summary>

React Helmet is a library that lets you **manage the `<head>` of your HTML document** from within your React components, things like `<title>`, `<meta>` tags, `<link>` tags, and `<script>` tags.

</details>

<details>
<summary>What is the different between <code>controlled</code> and <code>uncontrolled elements</code>?</summary>

- Controlled — React owns the state, The input's value is driven entirely by React state. Every keystroke goes through React

```javascript
function ControlledForm() {
  const [name, setName] = useState("");

  return (
    <input
      value={name} // React controls the value
      onChange={(e) => setName(e.target.value)} // React updates on change
    />
  );
}
// User types → onChange fires → setState → React re-renders → input updates
```

- Uncontrolled — the DOM owns the state, You let the browser manage the input naturally, and read the value when you need it via a `ref`.

```javascript
function UncontrolledForm() {
  const inputRef = useRef(null);

  function handleSubmit() {
    console.log(inputRef.current.value); // read on demand
  }

  return (
    <>
      <input ref={inputRef} defaultValue="initial" />
      <button onClick={handleSubmit}>Submit</button>
    </>
  );
}

// User types → DOM updates itself → React not involved
// Submit → ref reads current DOM value
```

</details>

<details>
<summary>What are error boundaries in React for?</summary>

Error boundaries are a feature in React that help manage and handle errors in a more graceful way. They allow developers to catch JavaScript errors anywhere in their component tree, log those errors, and display a fallback UI instead of crashing the entire application.

To create an error boundary, you need to define a class component that implements either or both of the following lifecycle methods:

- `static getDerivedStateFromError(error)`: This method is used to update the state so the next render will show the fallback UI.
- `componentDidCatch(error, info)`: This method is used to log error information.

```javascript
// implementation
class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render shows the fallback UI
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // You can also log the error to an error reporting service
    console.error("Error caught by ErrorBoundary: ", error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}

export default ErrorBoundary;

// Usage
<ErrorBoundary>
  <MyComponent />
</ErrorBoundary>;
```

- **What error boundaries do NOT catch:**
  - **Event handlers** — use `try/catch` inside the handler
  - **Async code** — `setTimeout`, promises, `fetch`
  - **Server-side rendering**
  - **Errors in the error boundary itself**

  They only catch errors during **rendering**, **lifecycle methods**, and **constructors** of the tree below them.

- **How to handle errors outside of boundaries:**
  For event handlers and async errors, use regular `try/catch` and state-based error UI:

- **Next.js error handling:**
  - `error.js` (App Router) acts as an error boundary for its route segment — under the hood it wraps your `page.js` in a React error boundary. Same limitations apply (catches render errors, not event handler errors).
  - `global-error.js` — catches errors in the root layout
  - Each route segment can have its own `error.js` to catch errors in that subtree
  - `error.js` receives two props: `error` (the Error object) and `reset` (function to retry rendering the segment)

- **`error.digest` and dev vs prod:**
  - `error.digest` is a unique hash auto-generated by Next.js for each error. In production, server-side error messages are **stripped for security** — only the digest is sent to the client so you can correlate it with server logs.

  | | Dev | Prod |
  |---|---|---|
  | `error.message` | Full message | Generic (stripped) |
  | `error.stack` | Full stack trace | Not available |
  | `error.digest` | Present | Present (use to match server logs) |
  | Error overlay | Next.js error overlay | No overlay, your `error.js` fallback |

  The production pattern: log `error.digest` on the client (send to Sentry, etc.) and match it against server-side logs where the full error details live.

</details>

<details>
<summary>What is React Suspense and what does it enable?</summary>

Suspense lets a component "suspend" rendering while waiting for something async (data, code, etc.). React **unmounts** the children and shows the `fallback` until the async work resolves.

- **How it works under the hood:** a component throws a Promise → React catches it at the nearest `<Suspense>` boundary → shows fallback → re-renders when the promise resolves.

- **Code splitting with `React.lazy`**

```javascript
const LazyComponent = React.lazy(() => import("./LazyComponent"));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
  );
}
```

- **Data fetching — `useSuspenseQuery` vs `useQuery`**

  | | `useQuery` | `useSuspenseQuery` |
  |---|---|---|
  | Returns | `{ data, isLoading, error }` | `{ data }` — always defined |
  | Loading state | You handle it manually | Delegates to `<Suspense>` boundary |
  | Error state | You handle it manually | Delegates to error boundary |
  | Suspense compatible | No (doesn't throw a promise) | Yes (throws a promise) |

```javascript
// useQuery — manual loading/error handling
function DataComponent() {
  const { data, isLoading, error } = useQuery({ queryKey: ["data"], queryFn: fetchData });

  if (isLoading) return <Spinner />;
  if (error) return <Error />;
  return <div>{data.name}</div>;
}

// useSuspenseQuery — Suspense handles loading, error boundary handles errors
function DataComponent() {
  const { data } = useSuspenseQuery({ queryKey: ["data"], queryFn: fetchData });
  return <div>{data.name}</div>; // data is always defined here
}

// wrap it
<ErrorBoundary fallback={<Error />}>
  <Suspense fallback={<Spinner />}>
    <DataComponent />
  </Suspense>
</ErrorBoundary>
```

- **Suspense shows fallback, NOT an overlay**
  Suspense **unmounts** children and replaces them with the fallback — you can't show a loading overlay on top of stale content with Suspense alone. For that, use `useTransition`:

```javascript
function SearchResults({ query }) {
  const [isPending, startTransition] = useTransition();

  function handleSearch(newQuery) {
    startTransition(() => {
      setQuery(newQuery); // marks this update as non-urgent
    });
  }

  return (
    <div style={{ opacity: isPending ? 0.5 : 1 }}> {/* overlay effect */}
      <Results query={query} />
    </div>
  );
}
// isPending = true while React renders the new tree in the background
// Old UI stays visible (dimmed), no unmount, no fallback
```

- **Streaming SSR** — Suspense boundaries also define streaming chunks in Next.js. Server sends HTML for resolved parts immediately, suspended parts stream in as they resolve.

</details>
