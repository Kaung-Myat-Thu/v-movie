<template>
  <Header />
  <main>
    <router-view />
  </main>
</template>

<script>
import Header from "./components/Header.vue";
export default {
  components: {
    Header,
  },
};
</script>

<style>
body {
  background: rgba(0, 0, 0, 0.5);
}
</style>
