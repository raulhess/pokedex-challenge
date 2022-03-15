<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-toolbar-title style="font-weight: 700">
          Pokédex Challenge
        </q-toolbar-title>

        <q-btn flat dense round icon="menu" aria-label="Menu" />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "MainLayout",
});
</script>
