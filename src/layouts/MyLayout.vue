<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-primary text-white">
      <q-toolbar>
        <q-avatar>
          <img src="assets/logo.png" style="width: 48px; height: 48px;">
        </q-avatar>

        <q-toolbar-title>
          Diadem Challenge
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<style>
</style>

<script>
export default {
  name: 'MyLayout'
}
</script>

<style>
</style>
