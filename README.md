# vue-components-communication-with-events

In Vue 3, components communicate with events using the Composition API and the <script lang="ts" setup> syntax. The Composition API provides a set of functions and reactive data structures that allow you to organize and reuse component logic more effectively.

To understand how components communicate with events using the Composition API, let's consider an example. Suppose you have a parent component that emits an event, and a child component that listens to that event.

In the parent component, you can define an event using the defineEmits function from the Composition API. This function allows you to declare the events that the component can emit. Here's an example:

## Parent Component
  
```vue
<!-- ParentComponent.vue -->
<template>
  <div>
    <ChildComponent @custom-event="handleCustomEvent" />
    <p>{{ payloadMessage }}</p>
  </div>
</template>

<script lang="ts" setup>
import { defineEmits, ref } from "vue";
import ChildComponent from "./ChildComponent.vue";

defineEmits(["custom-event"]);

const payloadMessage = ref(""); // Create a reactive variable to hold the payload message

const handleCustomEvent = (payload: unknown) => {
  console.log("Received custom event:", payload);
  payloadMessage.value = String(payload); // Update the payload message variable
};
</script>
```
  
## Child Component
  
```vue
<!-- ChildComponent.vue -->
<template>
  <button @click="emitCustomEvent">Emit Custom Event</button>
</template>

<script lang="ts" setup>
import { defineEmits } from "vue";

const emit = defineEmits(["custom-event"]);

const emitCustomEvent = () => {
  const payload = "Hello from ChildComponent!";
  emit("custom-event", payload);
};
</script>
```

In this example, the parent component emits an event called 'message' when the button is clicked, passing the message 'Hello from parent!'. The child component listens to the 'message' event using the on function and logs the received message to the console.

Note that you can also pass data along with the event by providing additional arguments to the emits function. In the example above, we passed the message as the second argument to emits('message', 'Hello from parent!'), and it was received as the message parameter in the child component's event listener.

By using the Composition API and the <script lang="ts" setup> syntax, you can effectively communicate between components using events in Vue 3.
  
## App.vue component

```vue
<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <ParentComponent />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ParentComponent from "./components/ParentComponent.vue";

export default defineComponent({
  name: "App",
  components: {
    ParentComponent,
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
