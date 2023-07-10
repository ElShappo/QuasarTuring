<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="q-pa-lg text-weight-light">
      <q-toolbar class="">
        <q-toolbar-title class="text-weight-light">
          <q-btn flat square no-caps class="text-weight-light" to="/"
            ><div class="text-h4 text-weight-light">Turing Machine</div></q-btn
          >
        </q-toolbar-title>

        <q-btn flat round dense icon="settings" class="q-mr-xs" to="/settings">
          <q-tooltip> Settings </q-tooltip>
        </q-btn>
        <q-btn flat round dense icon="help" to="/help">
          <q-tooltip> Help </q-tooltip>
        </q-btn>
        <q-btn-dropdown
          color="primary"
          label="eng"
          square
          flat
          class="text-white"
          ripple
        >
          <q-list>
            <q-item clickable v-close-popup @click="onItemClick">
              <q-item-section>
                <q-item-label>English</q-item-label>
              </q-item-section>
            </q-item>

            <q-item clickable v-close-popup @click="onItemClick">
              <q-item-section>
                <q-item-label>Russian</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
      </q-toolbar>
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

  setup() {
    return {
      onItemClick() {
        console.log("clicked item!");
      },
    };
  },
});
</script>
