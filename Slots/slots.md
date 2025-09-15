# What are slots in Vue.js? How do they work?

"Slots in Vue.js are a way to pass content from a parent component into a child component. They work like placeholders inside the child. 

For example, if we create a `Card` component with a `<slot>` tag inside, then when we use that component, we can put any custom content between the opening and closing tags, and Vue will render it in that place.

There are different types of slots. The default slot is just one placeholder for any content. Named slots let me have multiple placeholders, for example one for header and one for footer. And scoped slots allow the child to expose some data to the parent, so the parent can render that data the way it wants.

So basically, slots give flexibility — instead of hardcoding markup inside a component, I can make it reusable and allow the parent to decide what content goes inside."

---

# What is the difference between default and named slots ?

"A default slot is the simplest one. If I put just `<slot></slot>` inside a child component, Vue will replace it with whatever content I pass between the opening and closing tags of that component.

Named slots are used when I need more than one slot. For example, I can define `<slot name='header'></slot>` and `<slot name='footer'></slot>` inside a child. Then, in the parent, I wrap my content in `<template v-slot:header>` or `<template v-slot:footer>` to decide where it goes.

So the difference is: the default slot is only one and doesn’t need a name, while named slots allow me to create multiple placeholders and control exactly which part of the child they should fill."

---

Отличный вопрос! 🎯 Давай я дам тебе устный вариант ответа, чтобы на интервью звучало понятно и уверенно:

---

# How do we pass data to slots (scoped slots) ?

"Scoped slots are used when the child component wants to share some data with the parent through a slot. The idea is that the child exposes data, and the parent decides how to render it.

For example, inside the child I can write:

```vue
<slot :user='user'></slot>
```

Here I’m passing the `user` object to the slot.

Then in the parent, when I use this component, I can write:

```vue
<template v-slot:default='{ user }'>
  <p>{{ user.name }}</p>
</template>
```

So the child provides the data, but the parent has full control over how it looks. That’s very powerful for reusable components, like tables or lists, because the component gives the data, and the parent decides how to display it."




