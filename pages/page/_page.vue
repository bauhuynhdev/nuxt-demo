<template>
  <div>
    <ul>
      <li v-for="item in items">{{ item.id }} - {{ item.title }}</li>
    </ul>
    <ul class="pagination">
      <li v-for="page in pages">
        <NuxtLink :to="'/page/' + page">{{ page }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  async asyncData({$axios, route}) {
    const page = route.params.page || 1;
    const perPage = 15;
    const start = (page - 1) * perPage;
    const end = page * perPage;
    const {data} = await $axios.get('https://jsonplaceholder.typicode.com/posts');
    const total = data.length;
    const items = data.slice(start, end)
    const pages = Math.round(total / perPage);
    return {
      items,
      total,
      pages
    }
  }
}
</script>

<style scoped>
.pagination {
  list-style: none;
}

.pagination li {
  float: left;
  padding-right: 15px;
}
</style>