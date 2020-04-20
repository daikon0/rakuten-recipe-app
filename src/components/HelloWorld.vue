<template>
  <ul>
    <li v-for="category in categories" :key="category.categoryId">
      <router-link :to="{name:'category', params:{id:category.categoryId}}">{{ category.categoryName }}</router-link>
    </li>
  </ul>
</template>

<script>
const axios = require('axios')
export default {
  name: 'HelloWorld',
  data: () => ({
    categories: []
  }),
  created: async function () {
    try {
      const category = await axios.get(`https://app.rakuten.co.jp/services/api/Recipe/CategoryList/20170426?applicationId=${process.env.VUE_APP_RAKUTEN}&categoryType=large`)
      this.categories = category.data.result.large
    } catch (err) {
      alert(JSON.stringify(err))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
