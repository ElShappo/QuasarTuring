<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="text-center q-pa-lg text-h3 text-weight-light">
      Turing Machine
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "MainLayout",

  setup() {},
});
</script>
