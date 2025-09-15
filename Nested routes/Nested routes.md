# How do nested routes work?

"Nested routes in Vue Router let us build a route inside another route, which is useful for layouts and pages that have sub-sections.

In the route configuration, I can define a `children` array inside a parent route. Each child route will be rendered inside the parent’s `<router-view>`.

For example, if I have a `/users` route with children like `/users/profile` or `/users/settings`, I define them as child routes. Then in the `Users` component template I put a `<router-view>`. That’s where the nested child component will appear.

So the parent route acts like a container, and the child routes fill in the inner `<router-view>`. This makes it easy to create multi-level pages with shared layout."


---



# What is a dynamic path in Vue Router? How does it work?

"A dynamic path in Vue Router means that part of the URL is variable, so the same route can handle different values.

We define it using a colon in the path. For example, `/users/:id` will match `/users/1`, `/users/25`, or any other `id`. Inside the component, I can access that value with `this.$route.params.id`.

Dynamic paths are useful for pages like user profiles, product details, or anything that depends on an ID or a slug.

We can also have multiple dynamic segments, like `/users/:id/posts/:postId`. Vue Router will parse them and put them into `params`, so I can use them directly in my component logic."

