<template>
  <q-virtual-scroll
    :items="heavyList"
    virtual-scroll-horizontal
    v-slot="{ item, index }"
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

<script>
const maxSize = 100;
const heavyList = [];

for (let i = 0; i < maxSize; i++) {
  heavyList.push({
    class: "q-pa-md self-center ",
  });
}

export default {
  setup() {
    return {
      heavyList,
    };
  },
};
</script>

<style>
.cell {
  border: 1px solid black;
}
</style>
