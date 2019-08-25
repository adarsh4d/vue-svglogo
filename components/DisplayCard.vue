<template>
  <div :class="{span2:landscape}">
    <div class="card" @click="downloadFile">
      <img :src="`/logos/${files}`" width="100%" />
    </div>
    <a :href="url">
      <p class="title">{{title}}</p>
    </a>
  </div>
</template>

<script>
import download from 'downloadjs'
export default {
  props: {
    files: {
      type: String,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    landscape: {
      type: Boolean,
      default: false,
      required: false
    },
    url: {
      type: String,
      required: true
    },
    shortname: {
      type: String,
      required: true
    }
  },
  methods: {
    downloadFile() {
      download(`/logos/${this.files}`)
    }
  }
}
</script>

<style scoped>
.card {
  display: flex;
  background: #fff;
  padding: 12px;
  border-radius: 4px;
  box-shadow: 0 2px 4px #36466310, 0 0 1px #e4e9f2;
  height: 115px;
  cursor: pointer;
}
.card:hover {
  box-shadow: 0 4px 6px -1px #36466310, 0 2px 4px -1px #e4e9f2;
}
.title {
  text-align: center;
  margin: 8px auto 0;
  cursor: pointer;
  color: #343a40;
}
.span2 {
  grid-column: span 2;
}
</style>