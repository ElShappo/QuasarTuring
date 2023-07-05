<template>
  <div class="text-h3 q-pt-xl text-weight-light full-width text-center">
    <slot name="title"></slot>
  </div>
  <div class="q-gutter-sm q-pt-md">
    <q-radio v-model="shape" val="line" label="One way tape" />
    <q-radio v-model="shape" val="rectangle" label="Two ways tape" />
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
      <div class="text-subtitle2">{{ index }}</div>
    </div>
  </q-virtual-scroll>
</template>

<script setup>
import { ref, onMounted } from "vue";

const maxSize = 100;
const heavyList = [];

for (let i = 0; i < maxSize; i++) {
  heavyList.push({
    class: "q-pa-md self-center ",
  });
}
const virtualScroll = ref(null);

onMounted(() => {
  virtualScroll.value.scrollTo(50, "center-force");
});
</script>

<style>
.cell {
  border: 1px solid black;
}
</style>
