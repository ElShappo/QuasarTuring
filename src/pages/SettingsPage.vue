<template>
  <div class="text-h4 q-pt-lg q-pb-md text-weight-light full-width text-center">
    <q-icon name="settings" class="q-pb-xs q-pr-sm" /><span
      >Settings & View</span
    >
  </div>

  <div
    class="row justify-center items-center full-width text-h6 text-weight-light"
  >
    <div class="row items-center justify-center col-12 q-pb-md">
      <div class="offset-5"></div>
      <div class="col-5 offset-3 row items-center">
        <div>Tape direction:</div>
        <q-radio
          v-model="tapeDirection"
          val="oneWay"
          label="one way tape"
          size="sm"
        />
        <q-radio
          v-model="tapeDirection"
          val="twoWay"
          label="two way tape"
          size="sm"
        />
      </div>
      <div class="offset-5"></div>
      <div class="col-5 offset-3">
        <q-checkbox
          left-label
          v-model="isIndex"
          label="Display indices:"
          size="sm"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
const tapeDirection = ref("oneWay");
const isIndex = ref(true);
</script>
