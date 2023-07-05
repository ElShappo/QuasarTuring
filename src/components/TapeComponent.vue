<template>
  <div class="text-h3 q-pt-xl q-pb-sm text-weight-light full-width text-center">
    <slot name="title"></slot>
  </div>

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

  <q-virtual-scroll
    :items="heavyList"
    virtual-scroll-horizontal
    v-slot="{ item, index }"
    ref="virtualScroll"
  >
    <div
      :key="index"
      :class="item.class"
      class="text-h4 text-weight-thin text-grey cell q-px-lg text-center"
    >
      <div>λ</div>
      <div v-if="isIndex && tapeDirection === 'oneWay'" class="text-subtitle2">
        {{ index }}
      </div>
      <div
        v-else-if="isIndex && tapeDirection === 'twoWay'"
        class="text-subtitle2"
      >
        {{ index - Math.floor(maxSize / 2) }}
      </div>
    </div>
  </q-virtual-scroll>
</template>

<script setup>
import { ref, onMounted, watch } from "vue";

const maxSize = 101;
const heavyList = [];

for (let i = 0; i < maxSize; i++) {
  heavyList.push({
    class: "q-pa-md self-center ",
  });
}
const virtualScroll = ref(null);
const tapeDirection = ref("oneWay");
const isIndex = ref(true);

onMounted(() => {
  virtualScroll.value.scrollTo(0);
});

watch(tapeDirection, (newTapeDirection) => {
  if (newTapeDirection === "oneWay") {
    virtualScroll.value.scrollTo(0);
  } else {
    virtualScroll.value.scrollTo(Math.floor(maxSize / 2), "center-force");
  }
});
</script>

<style>
/* .cell {
  border: 1px solid black;
} */
</style>
