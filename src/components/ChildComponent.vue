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
