---
title: 'Error Boundaries in React'
date: '2023-01-31'
tags: ['react', 'error-boundary', 'javascript']
---

Sometimes in react applications, when an unexpected error happens in production, and there is no fallback UI to handle that state of the app, the entire page becomes just white, which in turn is a confusing experience for the end-user, as he in doesn’t know if the page is still loading or what exactly is going.

The 2 types of error message thrown at the console are like this:

First is adding a `<Suspense />` component - which lets you "wait" for some code to load and declaratively specify a loading state ( e.g. a spinner ) while we're waiting.

![Error_boundary_1](/static/images/error-boundaries-in-react/error-boundary-1.png)

![Error_boundary_2](/static/images/error-boundaries-in-react/error-boundary-3.png)

Second is the suggestion to add an [Error Boundary](https://reactjs.org/docs/error-boundaries.html) Component. As defined in the react docs, this component lets us **catch Javascript errors anywhere in the child component tree, log these errors, and provide a fallback UI,** when an error in UI part happens.

The way to implement this component in a react application is by using the class-based component approach. This is needed because to become an error boundary the component should specify either of the 2 methods - the static _getDerivedStateFromError_ or _componentDidCatch,_ lifecycle method.

```tsx
import { Component } from 'react'
interface ErrorBoundaryProps {}

interface ErrorBoundaryState {
  hasError: boolean
  errorMessage: string
}

// class based components in typescript inherit from the generic Component class
// which requires 2 types ComponentProps type, and ComponentState type.
class ErrorBoundary extends Component<ErrorBoundaryProps, ErrorBoundaryState> {
  constructor(props: ErrorBoundaryProps) {
    super(props)
    this.state = { hasError: false, errorMessage: '' }
  }

  static getDerivedStateFromError() {
    // Update state so the next render will show the fallback UI.
    console.error(error)
    return { ...this.state, hasError: true }
  }
  componentDidCatch(error, errorInfo) {
    // log the error also in the logging service, for further introspection
    // You can also log the error to an error reporting service
    logErrorToMyService(error, errorInfo)
    return { ...this.state, errorMessage: errorInfo }
  }
  render() {
    if (this.state.hasError) {
      return <h1>An unexpected error has happened 🤷. Please refresh 🔄 the page</h1>
    }

    return this.props.children
  }
}

export default ErrorBoundary
```

After defining it we can use it in our application like so

```jsx
<ErrorBoundary>
  <App />
</ErrorBoundary>
```

So now if we introduce an ‘accidental’ error in our app.

```jsx
// App.tsx
throw new Error('test error')
```

We have the following fallback UI in the page, rendered by the ErrorBoundary component.

![Error_bounday_3](/static/images/error-boundaries-in-react/error-boundary-2.png)

One important note **As of React 16, errors that were not caught by any error boundary will result in unmounting of the whole React component tree.**

To summarize, error boundary components are a useful tool in gracefully handling unforeseen errors in production environment, enabling us to provide a fallback UI, instead of just a blank page.
