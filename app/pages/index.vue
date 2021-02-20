<template>
  <div class="container">
    <ul>
      <li v-for="content in contents" :key="content.id">
        <nuxt-link :to="`/${content.id}`">
          {{ content.title }}
        </nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data() {
    return {
      contents: [],
    }
  },
  async asyncData({ $axios }) {
    const { data } = await $axios.get(
      'https://nuxtsampleproduct.microcms.io/api/v1/news',
      {
        headers: { 'X-API-KEY': '35d930d3-1783-410b-b4df-698d147242c4' },
      }
    )
    return { contents: data.contents }
  },
})
</script>

<style scoped>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.links {
  padding-top: 15px;
}
</style>
