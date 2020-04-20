<template>
  <div class=recipe>
    <h2>aaa</h2>
    <ul>
      <li v-for="recipe in recipes" :key="recipe.recipeId">
        <img :src="recipe.foodImageUrl"> {{ recipe.recipeTitle }}
      </li>
    </ul>
  </div>
</template>

<script>
const axios = require('axios')
export default {
  name: 'Ranking',
  data: () => ({
    recipes: []
  }),
  created: async function () {
    try {
      const recipe = await axios.get(`https://app.rakuten.co.jp/services/api/Recipe/CategoryRanking/20170426?applicationId=${process.env.VUE_APP_RAKUTEN}&categoryId=${this.$route.params.id}`)
      this.recipes = recipe.data.result
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
