---
title: 'An intro to React Context'
date: '2023-01-25'
image: '/static/images/ReactContext.png'
tags: ['react', 'react_context']
---

![React Context Example](/static/images/ReactContext.png)

## So what’s react context ?

As defined in React docs

[Context - React](https://reactjs.org/docs/context.html)

> Context provides a way to pass data through the component tree without having to pass props down manually at every level.

The problem that arises when passing props acrossing components that are multiple levels deep in the inheritance hierarchy is the so-called **"prop-drilling”**.

Say we have an interface for an object called _ICart_

```tsx
interface ICart {
  slider_enabled: boolean
  settings: CartSettings
}
interface CartSettings {
  [CartNavigationEnum.design]: CartDesignSettings
  /// other settings
}
```

and we have a component hierarchy in an application that uses a card editor to visually change the look of a shopping cart that looks like this:

```tsx
<CartEditor cart={cart} />
 |
 |
    <CartEditorNavigation cart={cart} />
        |
        |
    <SelectedSettingsComponent cart={cart}>
        |
        |
            <CartEditorAnnouncement cart={cart}>
                |
                |
                <FeatureActivity enabled={cart.announcement.enabled}>
```

As we see the Feature Activity component is concerned whether the cart announcement is enabled. From this hierarchy we need to pass our state variable cart - multiple levels deep which results in prop-drilling. A better approach would be to create a custom React context, and use the specific pieces of the object that are relevant for the component.

```tsx
interface CartContextProps {
  cart: ICart
  saved: boolean
  loading: boolean
}

const CartContext = React.createContext<CartContextProps>({
  cart: initial_cart,
  saved: true,
  loading: false,
})
```

Here we create a context object that stores 3 specific state variables, the cart object, saved boolean, whether the cart editing is saved or not and loading boolean variable.

Then we need to create a provider component that will expose all these variables to its children

```tsx
const CustomCartContextProvider = (props: any) => {
  return (
    <CartContext.Provider
      value={{
        cart: tempCart,
        saved: isSaved,
        loading,
      }}
    >
      {props.children}
    </CartContext.Provider>
  )
}
```

After this step is completed we need to wrap the root CartEditor component with our custom context provider component.

```tsx
<CustomCartContextProvider>
  <CartEditor />
</CustomCartContextProvider>
```

So now insted of having to pass props in the inheritance hierarchy we can just use the special _**useContext**_ hook provided by the react library and destructure the parts of the context we’re interested in.

```tsx
// CartEditorAnnouncement.tsx

const CartEditorAnnouncment = () => {
  const {
    cart: {
      settings: { announcements },
    },
    onAnnouncementSettingsChange,
  } = useContext(CartContext)

  return <FeatureActivity enabled={announcements.enabled} />
}
```

In this case by using the context we have decoupled the coupling between components in the component inheritance hierarchy.
