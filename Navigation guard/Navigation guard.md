# What is a Navigation Guard in Vue Router? How do we use custom guards?

"Navigation guards in Vue Router are functions that let us control access to routes. They run before, during, or after a navigation, and they decide if the user can go to a route, should be redirected, or blocked.

There are three main types:

* **Global guards**, like `router.beforeEach`, which apply to every route change.
* **Per-route guards**, which are defined directly in the route config.
* **In-component guards**, like `beforeRouteEnter` or `beforeRouteLeave`.

For example, if I want only logged-in users to see a dashboard, I can write a custom guard in `router.beforeEach` that checks authentication. If the user is not logged in, I redirect them to `/login`.

Custom guards are just functions where we add our own logic — usually checking tokens, roles, or permissions — and then we call `next()` to allow navigation, or pass a different route to redirect.

So basically, navigation guards are Vue Router’s way of protecting and controlling navigation flow, and custom guards let us apply our own business rules."



---



# What are the basic router hooks ?

"In Vue Router we have several built-in navigation guards, or router hooks, that control the flow when navigating between routes. The most basic ones are:

* **Global guards**:

  * `beforeEach` → runs before every navigation. Good for authentication checks.
  * `afterEach` → runs after navigation is confirmed. Useful for logging or analytics.

* **Per-route guards**:

  * `beforeEnter` → defined directly in the route config, only runs when entering that specific route.

* **In-component guards**:

  * `beforeRouteEnter` → called before entering the route that renders this component.
  * `beforeRouteUpdate` → called when the route changes but the same component is reused.
  * `beforeRouteLeave` → called when leaving the route.

Together, these hooks give us full control over navigation: we can block, redirect, or run side effects depending on the situation."



---



# How do you create a custom navigation guard ?

"To create a custom guard, I usually add logic inside the router configuration or in a global guard.

For example, if I want to check authentication globally, I can use `router.beforeEach`. Inside the function, I check if the target route requires auth. If yes, and the user is not logged in, I redirect them to `/login`. Otherwise, I call `next()` to continue.

Here’s the idea in code:

```js
router.beforeEach((to, from, next) => {
  const isAuthenticated = !!localStorage.getItem('token')
  if (to.meta.requiresAuth && !isAuthenticated) {
    next('/login')
  } else {
    next()
  }
})
```

I can also define a per-route guard with `beforeEnter` directly in the route config, if only one route needs this check.

So a custom guard is basically any function where I put my own business logic — authentication, roles, permissions — and then control the navigation with `next()`."





---



# What is the difference between a guard and a resolver?


"A navigation guard controls *whether* a route can be accessed. It runs before navigation and can allow, block, or redirect the user. For example, a guard checks if the user is logged in before showing the dashboard.

A resolver, on the other hand, is about *data*. It runs before the route is entered, and its job is to fetch or prepare the data that the component needs. The route will only be activated after the resolver finishes, so the component always has the required data when it’s created.

So the difference is:

* **Guard → access control** (yes/no/redirect).
* **Resolver → data preparation** (make sure data is ready before rendering)."




---



# What is metadata on a route ?

"In Vue Router, metadata is extra information we can attach to a route using the `meta` field in the route config.

For example, I can write:

```js
{
  path: '/dashboard',
  component: Dashboard,
  meta: { requiresAuth: true, role: 'admin' }
}
```

This doesn’t affect routing by itself — it’s just custom data. But we can use it inside navigation guards. For instance, in a global `beforeEach` guard, I can check `to.meta.requiresAuth` to decide if the user needs to be logged in.

So basically, metadata is a flexible way to store custom info about a route, like authentication, permissions, page titles, breadcrumbs, or even layout options."




---



# How can we add animation when changing routes in Vue.js?

"In Vue we can animate route transitions using the built-in `<transition>` component around `<router-view>`.

For example, I wrap `<router-view>` like this:

```vue
<transition name='fade' mode='out-in'>
  <router-view />
</transition>
```

Then I define CSS for that transition, for example:

```css
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
```

This way, when I navigate between routes, the old component fades out and the new one fades in.

I can also use libraries like Animate.css or custom transitions to make more complex effects.

So the idea is: wrap `<router-view>` in `<transition>`, give it a name, and define CSS animations for enter and leave."



---




# How does scroll behavior work with routes in Vue Router?

"Vue Router lets us control the scroll position when navigating between routes by using the `scrollBehavior` function in the router configuration.

By default, when we switch routes, the scroll position stays the same. But sometimes we want a different behavior — for example, always scroll to the top, or restore the saved position when using the browser’s back and forward buttons.

The `scrollBehavior` function receives three arguments: `to`, `from`, and `savedPosition`. If `savedPosition` exists, it means the user is navigating with back/forward, so we can return it to restore the previous scroll. Otherwise, we can return `{ left: 0, top: 0 }` to scroll to the top.

For example:

```js
const router = new VueRouter({
  routes,
  scrollBehavior(to, from, savedPosition) {
    if (savedPosition) {
      return savedPosition
    } else {
      return { left: 0, top: 0 }
    }
  }
})
```

So with `scrollBehavior`, we have full control of the scroll position after navigation."



---



# What is lazy loading in Vue Router?

"Lazy loading means that we load route components only when they are needed, instead of putting everything in the main bundle. This improves performance, especially for large apps.

In Vue Router, we do this by using dynamic imports. Instead of importing a component at the top, we define the component in the route like this:

```js
const router = new VueRouter({
  routes: [
    {
      path: '/about',
      component: () => import('@/views/About.vue')
    }
  ]
})
```

Here, the `About` component will be loaded only when the user navigates to `/about`.

The benefit is that the initial load of the app becomes faster, because not all pages are bundled together. Vue and Webpack automatically split the code into chunks and load them on demand."





