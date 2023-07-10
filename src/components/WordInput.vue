<template>
  <div class="q-pa-md" style="max-width: 300px">
    <q-input v-model="wordOnTape" filled autogrow :label="title" />
  </div>
</template>

<script setup>
import { ref } from "vue";
const props = defineProps({
  title: String,
});

let wordOnTape = ref("");
</script>
