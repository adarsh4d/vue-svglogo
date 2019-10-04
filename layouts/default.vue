<template>
  <div>
    <a href="#skipped-content" class="btn-skip">Skip to main Content</a>
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
.btn-skip {
  position: fixed;
  left: 0;
  right: 0;
  background: #0066ff;
  color: #ffffff;
  top: -50px;
  text-align: center;
  padding: 10px;
}
.btn-skip:active,
.btn-skip:focus {
  top: 0;
}
</style>