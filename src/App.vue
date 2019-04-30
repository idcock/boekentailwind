<template>
  <div id="app">
    <Titel />
    <main class="container mx-auto py-4">
      <router-view />
    </main>
  </div>
</template>

<script>
import Titel from "@/layouts/Titel.vue";

export default {
  components: {
    Titel
  }
};
</script>

<style></style>
