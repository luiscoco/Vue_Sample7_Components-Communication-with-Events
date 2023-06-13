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
