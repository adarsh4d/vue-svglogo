<template>
  <main>
    <div class="banner">
      <h1>{{logos.length}} High-quality SVG logos</h1>
    </div>
    <div class="container sticky">
      <div class="searchbar">
        <SearchIcon />
        <SearchFocus @keyup="focusSearch" />
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
      <div class="content">
        <Card v-for="l in result" :key="l.name" v-bind="l" />
      </div>
      <infinite-loading :identifier="result" @infinite="infiniteHandler" v-if="!query"></infinite-loading>
    </div>
  </main>
</template>

<script>
import Card from '~/components/DisplayCard.vue'
import SearchFocus from '~/components/utils/SearchFocus.vue'
import SearchIcon from '~/components/icons/search.vue'
import logos from '~/models/logos.json'
import InfiniteLoading from 'vue-infinite-loading'
export default {
  name: 'Home',
  components: {
    Card,
    SearchFocus,
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
    focusSearch(e) {
      if (e.key === "/") {
        this.$refs.search.focus()
      }
    },
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
</style>
