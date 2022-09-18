# React

React is a JavaScript library for rendering user interfaces (UI). 
UI can be represented in small units like buttons, text, and images.
React lets you combine them into reusable and nestable components.
React is used to render web and mobile and desktop native applications.
Compared to previous popular solutions, like jQuery, in a react application the developer declares 
the desired UI output using JSX instead of imperatively building or mutating DOM trees.

## Components model

A component must be pure, meaning:
1. It should not change any objects or variables that existed before rendering.
2. Given the same inputs, a component should always return the same JSX. 

You **should not mutate** any of the inputs that your components use for rendering. That includes props, state, and context. To update the screen, “set” state instead of mutating preexisting objects.
Strive to express your component’s logic in the JSX you return.
When you need to “change things”, you’ll usually want to do it in an `event handler`. 
As a last resort, you can `useEffect`.
Writing pure functions takes a bit of practice, but it unlocks the power of React’s paradigm.

## Trigger, Rendering and commit phases

### Trigger

#### Initial render

There are 3 reasons for a component to render:

1. It’s the component’s initial render.
2. The component’s state has been updated.
3. One of its dependencies tracked by react, context values or props, got updated.

During the initial render react generates an in memory representation of components tree, known as virtual DOM,
then creates the resulting DOM representation and mounts it using `appendChild()`.

#### Trigger updates

After the initial render, a subset of the UI can be updated changing a components' state.
When this action occurs, React queues a render. 

### Render

After you trigger a render, React calls your components to figure out what to display on screen. **“Rendering”** is React calling your components.

- **On initial render**, React will call the root component.
- **For subsequent renders**, React will call the function component whose state update triggered the render.

This process is recursive: if the updated component returns some other component, React will render that component next, and if that component also returns something, it will render that component next, and so on. 

The process will continue until there are no more nested components and React knows exactly what should be displayed on screen.

- During the initial render, React will create the DOM nodes necessary to represent the UI.
- During a re-render, React will calculate which parts of a virtual DOM tree have changed, if any, have changed since the previous render. 
It won’t do anything with that information until the next step, the commit phase.


see: [react docs](https://beta.reactjs.org/learn/render-and-commit#re-renders-when-state-updates)

### Commit phase

After a new representation of the state has been created

- **For the initial render**, React will use the `appendChild()` DOM API to put all the DOM nodes it has created on screen. 
- **For re-renders**, React will apply the minimal necessary changes to make the DOM match the latest rendering output.


### Recap

Any UI update in a React app happens in three steps:
- Trigger
- Render
- Commit

You can use Strict Mode to find mistakes in your components
React does not touch the DOM if the rendering result is the same as last time.

## useRef, imperative escape hatch

```ts
const refContainer = useRef(initialValue);
```

`useRef` returns a object with a mutable property `current` that is initially set to `initialValue` and
can be mutated.

- similar to useState `refContainer.current` value is persisted between renders.
- Changes to `refContainer.current` do not trigger renders.

### useRef - best practice

1. Consider useRef as an escape hatch to synchronize with external systems.
2. Don't read nor write ref during the rendering phase.
3. Do not use refs to render jsx.

2. 3. Are particularly important because react components must be pure and multiple invocations should yield the same output.

### Resources

- [https://beta.reactjs.org/apis/useref](https://beta.reactjs.org/apis/useref)
- [referencing values with refs](https://beta.reactjs.org/learn/referencing-values-with-refs)
- [https://reactjs.org/docs/hooks-reference.html#useref](https://reactjs.org/docs/hooks-reference.html#useref)

## Version changes

### React 17 notable changes

1. Synthetic events are no longer pooled, `evt.persist()` has no effect.
2. React no longer attaches event listeners at at the document but sets them at the root element instead, see [demo](https://stackblitz.com/edit/react-ts-evt-delegation).
3. new jsx transform to make `import * as React from 'react'` optional.
4. UseEffect cleanup is called asynchronously.

### Reat 18 notable changes

1. Suspense and lazy works in SSR environments.
2. React batches state updates outside event handlers too. e.g. `setTimeout(() => { setA(1); setB(2); }, 0)`.
3. Transitions, higher and lower priority rendering.
4. Rewritten suspense implementation.
5. New Api createRoot to opt-in to concurrent features.
6. New Hooks:
 - [`useId`](https://reactjs.org/docs/hooks-reference.html#useid) generates stable ids between SSR and client.
 - [`useSyncExternalStore`](https://reactjs.org/docs/hooks-reference.html#usesyncexternalstore) synchronization with external data sources that supports concurrent features.
 - [`useTransition`](https://reactjs.org/docs/hooks-reference.html#usetransition) marks state updates as transitions (lower priority).
   Updates in a transition yield to more urgent updates such as clicks.
 - [`useDeferredValue`](https://reactjs.org/docs/hooks-reference.html#usedeferredvalue) returns a deferred value of in input arg. It's like debounce without initial delay.


#### Transitions

A transition is a new concept in React to distinguish between urgent and non-urgent updates.

- Urgent updates reflect direct interaction, like typing, clicking, pressing, and so on.
- Transition updates transition the UI from one view to another.

Urgent updates like typing, clicking, or pressing, need immediate response to match our intuitions about how physical objects behave. 
Otherwise they feel “wrong”. 

However, transitions are different because the user doesn’t expect to see every intermediate value on screen.

Transitions can be initiated using:

- `startTransition`, imported from 'react'
- `[isTransitioning, startTransition] = useTransition()`