# What are refs?

"In Vue, refs are a way to directly access a DOM element or a child component instance. Normally, we use reactive data binding and don’t need to touch the DOM directly. But sometimes, for example if I need to focus an input, work with a third-party library, or measure an element’s size, I can use refs.

In the template, I add a `ref` attribute, like `<input ref='myInput' />`. Then in the script, I can access it using `this.$refs.myInput`. That gives me the raw DOM element.

If the ref is on a child component, then `$refs` will give me that component’s instance, so I can call its public methods.

The main idea is: refs are like shortcuts to DOM nodes or child components, but they should be used only when reactive binding is not enough."

---

Отличный вопрос 👌 Дам тебе устный вариант ответа, как на интервью:

---

# Why should we not interact with the DOM directly ?

"Vue is built around the idea of a virtual DOM and reactive data binding. When we change the data in Vue, it automatically updates the DOM for us in the most efficient way.

If we interact with the DOM directly, for example using `document.querySelector` or manually changing innerHTML, we bypass Vue’s reactivity system. That can lead to bugs, because Vue won’t know about those changes and might overwrite them on the next re-render.

Also, direct DOM manipulation breaks the separation of concerns: our logic should stay in the component and template, while Vue handles rendering.

Of course, sometimes we still need direct DOM access — like when using third-party libraries or APIs that require a DOM node. In those cases, we use `refs` instead of raw DOM methods, so Vue stays aware of what’s happening."

---

Хорошо 👍 Давай подготовим устный вариант ответа:

---

# What is `nextTick` ?

"`nextTick` is a Vue utility that lets me wait until the DOM has finished updating after a data change.

Vue updates the DOM asynchronously for performance reasons — it batches changes together. That means if I change some reactive data and immediately check the DOM, I might still see the old value.

When I use `Vue.nextTick` or in Vue 3 `nextTick` from Vue, I can pass a callback or use `await nextTick()`. This makes sure my code runs only after Vue has re-rendered the DOM.

For example, if I set a boolean to show a modal and then immediately want to focus an input inside that modal, I need `nextTick` to wait until the input actually exists in the DOM."


---



# What is `forceUpdate` ? What are the possible consequences of using it?

"`forceUpdate` is a method we can call on a Vue component to force it to re-render, even if Vue doesn’t detect any reactive changes.

Normally, Vue automatically re-renders only when reactive data changes. But if I’m working with something that is not reactive — for example, a property added later without `Vue.set` in Vue 2, or working with objects that Vue can’t track — I might use `this.$forceUpdate()` to refresh the view.

The consequences are that it bypasses Vue’s reactivity system and can hurt performance, because it forces a re-render even when it’s not really needed. It can also make the code harder to maintain, because it hides the real problem — usually we should fix reactivity instead of forcing updates.

So `forceUpdate` should only be used as a last resort, for edge cases, not in normal component logic."



---



# How does `inheritAttrs` work ?

"By default, Vue passes down all attributes from a parent component to the root element of the child component. For example, if I use `<MyButton class='red' />`, the `class` gets applied to the child’s root element.

Sometimes that behavior is not what we want — especially if the child has multiple elements or if we want to control where those attributes should go. In that case, we can set `inheritAttrs: false` in the child component’s options.

When we do this, Vue won’t automatically apply extra attributes to the root element. Instead, we can manually decide where to place them by using `$attrs`. For example, I can bind `$attrs` to a specific element inside my template, like `<button v-bind='$attrs'>`.

So basically, `inheritAttrs: false` gives us more control over attribute distribution, instead of always pushing them to the root element."



---




# What are `$parent` and `$children` ?

"`$parent` and `$children` are references that Vue gives us to navigate the component tree.

* `$parent` gives direct access to the parent component instance.
* `$children` gives an array of all direct child component instances.

For example, inside a child I can call `this.$parent` to access the parent’s data or methods. Or I can use `this.$children` in a parent to loop through and interact with its children.

But in practice, using `$parent` and `$children` is not recommended, because it creates tight coupling between components and makes them harder to maintain. The better way is to pass data with props, emit events, or use provide/inject.

So `$parent` and `$children` exist, but they’re more like escape hatches for special cases, not the main communication pattern in Vue."




