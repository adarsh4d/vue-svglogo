<template>
  <main>
    <div class="banner">
      <h1>{{logos.length}} High-quality SVG logos</h1>
    </div>
    <div class="container sticky">
      <div class="searchbar">
        <SearchIcon />
        <input
          type="search"
          ref="search"
          v-model="query"
          placeholder="Search logos (Press '/' to focus)"
          class="search"
          @keyup.esc="looseFocus"
        />
      </div>
    </div>
    <div class="container">
      <div class="content" v-if="result.length>0">
        <Card v-for="l in result" :key="l.name" v-bind="l" />
      </div>
      <div class="emptystate" v-else>
        <img src="/empty.png" alt="Search result empty" width="150px" />
        <h3>No logos found</h3>
        <p>Try adjusting your search to find what you're looking for.</p>
        <p class="subtitle">
          Logo not found? Request
          <a
            class="link"
            href="https://github.com/adarsh4d/vue-svglogo/issues"
          >here</a>
        </p>
      </div>
      <infinite-loading :identifier="result" @infinite="infiniteHandler" v-if="!query"></infinite-loading>
    </div>
    <div class="container">
      <p class="subtitle text-center">
        Made with by ❤️ by
        <a href="https://twitter.com/AdarshDK2">@AdarshDK2</a>
      </p>
    </div>
  </main>
</template>

<script>
import Card from '~/components/DisplayCard.vue'
import SearchIcon from '~/components/icons/search.vue'
import logos from '~/models/logos.json'
import InfiniteLoading from 'vue-infinite-loading'
export default {
  name: 'Home',
  components: {
    Card,
    SearchIcon,
    InfiniteLoading,
  },
  data() {
    return {
      logos,
      query: '',
      result: [],
    }
  },
  methods: {
    looseFocus(e) {
      this.$refs.search.blur()
    },
    infiniteHandler() {
      let length = this.result.length
      let temp = this.logos.slice(length, length + 100)
      this.result.push(...temp)
    },
    initalLoad() {
      this.result = this.logos.slice(0, 100)
    }
  },
  watch: {
    query() {
      window.scroll({ top: 0, left: 0, behavior: 'smooth' })
      if (this.query.trim() === "") {
        this.initalLoad()
      }
      else {
        this.$search(this.query, this.logos, { keys: ['shortname'], threshold: 0.1, })
          .then(res => { this.result = res })
      }
    }
  },
  mounted() {
    this.initalLoad()
    const MouseTrap = require('mousetrap')
    MouseTrap.bind('/', (e) => {
      e.preventDefault()
      this.$refs.search.focus()
    })
  }
}
</script>

<style>
.banner {
  display: flex;
  flex-direction: column;
  padding: 48px 24px 64px;
  background-color: #ffffff;
  border-bottom: 1px solid #e9ecef;
}
h1 {
  margin: 0 0 24px;
  font-size: 32px;
  font-weight: 400;
  line-height: 1.25;
  text-align: center;
}
.container {
  max-width: 1200px;
  margin: 0 auto;
}
.sticky {
  position: sticky;
  top: 0;
}
.searchbar {
  position: relative;
  padding: 16px 24px;
  background: #f8f9fa;
}
.feather-search {
  color: #c4c4c4;
  position: absolute;
  top: 28px;
  left: 40px;
}
.search::placeholder {
  color: #c4c4c4;
}
.loading {
  background: #00000030;
  z-index: 10;
  width: 100%;
}
input.search {
  width: 100%;
  box-sizing: border-box;
  box-shadow: 0 2px 4px #36466310, 0 0 1px #e4e9f2;
  border: 0;
  border-radius: 4px;
  appearance: none;
  padding: 16px;
  padding-left: 52px;
}
.content {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(115px, 1fr));
  grid-gap: 24px 16px;
  padding: 16px 24px;
  grid-auto-flow: row dense;
}
.emptystate {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  min-height: 300px;
  padding: 16px;
  box-sizing: border-box;
  text-align: center;
}
h3 {
  font-size: 26px;
  font-weight: normal;
  margin-bottom: 0;
  color: #1a202c;
}
p {
  font-size: 20px;
  margin-bottom: 0;
  color: #718096;
}
p.subtitle {
  margin-top: 30px;
  font-size: 16px;
}
a {
  color: #718096;
}
a.link {
  color: #0066ff;
}
.text-center {
  text-align: center;
}
</style>
