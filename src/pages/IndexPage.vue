<template>
  <q-page class="row justify-center items-center content-start bg-white">
    <TapeComponent>
      <template v-slot:title>Tape</template>
    </TapeComponent>
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
