<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar class="text-white shadow-2 rounded-borders">
        <q-btn flat label="Tarea 1 - Javascript" />
        <q-space />
        <div>Christian De Santis</div>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts">
</script>
