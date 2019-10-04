<template>
  <nav>
    <div>
      <nuxt-link to="/">
        <img src="/logo.svg" height="40px" alt="SVGVault logo" />
      </nuxt-link>
    </div>
    <div>
      <a
        class="link"
        href="https://twitter.com/intent/tweet?text=A%20collection%20of%201000+%20SVG%20vector%20logos%20https://svg-logo.netlify.com/"
        target="_blank"
        rel="noreferrer"
      >Tweet</a>
      <a
        class="link"
        href="https://github.com/adarsh4d/vue-svglogo"
        target="_blank"
        rel="noreferrer"
      >Github</a>
    </div>
  </nav>
</template>

<script>
export default {

}
</script>

<style scoped>
nav {
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
.link {
  color: #343a40;
}
</style>