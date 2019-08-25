<template>
  <header>
    <img src="/logo.svg" height="40px" alt="SVGVault logo" />
    <div>
      <a class="link" href="#">Tweet</a>
      <a class="link" href="#">Github</a>
    </div>
  </header>
</template>

<script>
export default {

}
</script>

<style scoped>
header {
  padding: 16px 24px;
  display: grid;
  grid-template-columns: 1fr auto;
  align-items: center;
  background-color: #ffffff;
}
.link + .link {
  padding-left: 10px;
}
.link:hover {
  color: #0066ff;
}
</style>