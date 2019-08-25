<template>
  <div>
    <Header />
    <nuxt />
  </div>
</template>

<script>
import Header from '~/components/PageHeader.vue'
export default {
  components: {
    Header
  }
}
</script>

<style>
html {
  font-family: "Roboto", sans-serif;
  box-sizing: border-box;
  color: #343a40;
  background: #f8f9fa;
}
</style>