<template>
  <q-page class="flex flex-center">
    <TapeComponent></TapeComponent>
    <CommandsInput></CommandsInput>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";
import TapeComponent from "src/components/TapeComponent.vue";
import CommandsInput from "src/components/CommandsInput.vue";

export default defineComponent({
  name: "IndexPage",
  components: {
    TapeComponent,
    CommandsInput,
  },
  setup() {
    const word = ref("");
  },
});
</script>
