<template>
  <main>
    <h1 class="title">{{ title }}</h1>
    <p>{{ publishedAt }}</p>
    <div v-html="body"></div>
  </main>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  data() {
    return {
      title: '',
      publishedAt: '',
      body: '',
    }
  },
  async asyncData({ params, $axios }) {
    const { data } = await $axios.get(
      `https://nuxtsampleproduct.microcms.io/api/v1/news/${params.slug}`,
      {
        headers: { 'X-API-KEY': '35d930d3-1783-410b-b4df-698d147242c4' },
      }
    )
    console.log(data)
    return {
      title: data.title,
      body: data.body,
      publishedAt: data.publishedAt,
    }
  },
})
</script>

<style scoped>
.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}
</style>
