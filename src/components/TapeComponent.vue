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
      class="virtual-scroll-cell text-h4 text-weight-thin text-grey q-px-lg text-center row justify-center"
      :tabindex="index + 1"
    >
      <div class="virtual-scroll-cell-content">λ</div>
      <div
        v-if="isIndex && tapeDirection === 'oneWay'"
        class="virtual-scroll-cell-index text-subtitle2"
      >
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

let cell = null;
let input = null;

onMounted(() => {
  virtualScroll.value.scrollTo(0);

  let virtualScrollElement = document.querySelector(
    ".q-virtual-scroll__content"
  );

  document.addEventListener("click", (event) => {
    if (!event.target.closest(".q-virtual-scroll__content") && cell) {
      cell.innerHTML = input.value;
      cell.classList.add("text-weight-light");
      input.remove();
    }
  });

  virtualScrollElement.addEventListener("click", (event) => {
    if (cell) {
      cell.innerHTML = input.value;
      cell.classList.add("text-weight-light");
      input.remove();
    }

    cell = event.target; // identify in which cell we are located at

    if (cell.classList.contains("virtual-scroll-cell")) {
      cell = cell.querySelector(".virtual-scroll-cell-content"); // go to cell content
    } else if (cell.classList.contains("virtual-scroll-cell-index")) {
      cell = cell.previousElementSibling; // go to virtual-scroll-cell-content div
    } else {
      // do nothing, already at position
    }

    let content = cell.innerHTML;

    input = document.createElement("input");
    input.style.width = cell.parentNode.clientWidth / 2 + "px";
    input.style.height = cell.clientHeight + "px";
    input.classList.add("text-center", "text-weight-light");
    input.value = content;

    cell.innerHTML = "";
    cell.appendChild(input);

    input.focus();
    input.select();

    input.addEventListener("input", (event) => {
      if (input.value.length > 1) {
        input.value = input.value[0];
      }
    });

    input.addEventListener("change", (event) => {
      if (input.value.length === 0) {
        input.value = "λ";
      } else {
        if (input.value !== "λ") {
          input.parentNode.classList.add("not-lambda");
        }
      }
    });
  });
});

watch(tapeDirection, (newTapeDirection) => {
  if (newTapeDirection === "oneWay") {
    virtualScroll.value.scrollTo(0);
  } else {
    virtualScroll.value.scrollTo(Math.floor(maxSize / 2), "start-force");
  }
});
</script>

<style>
.virtual-scroll-cell {
  border: 1px solid rgb(0, 0, 0);
  width: 2em;
}

.virtual-scroll-cell-content.not-lambda {
  color: black;
}
</style>
