<template>
  <div id="recipes"><br>
    <h1>Recipes</h1><br>
    <div v-if="recipes.length" id="recipe">
      <div v-for="recipe in recipes" :key="recipe.uuid" class="recipe">
       <router-link :to="{ name: 'RecipeDetails', params: { id: recipe.uuid} }">
          <h2>{{ recipe.title }}</h2>
       </router-link>
      </div>
    </div>
    <div v-else>
      <p>Loading recipes...</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      recipes: []
    }
  },
  mounted() {
    fetch('http://localhost:3001/recipes')
      .then(res => res.json())
      .then(data => this.recipes = data)
      .catch(err => console.log(err.message))
  }
}
</script>

<style>
  .recipe h2{
    background: #f4f4f4;
    padding: 20px;
    border-radius: 10px;
    margin: 10px auto;
    max-width: 600px;
    cursor: pointer;
    color: #000
  }
  .recipe h2:hover {
    background: #ddd;
  }
  .recipe a, .recipe{
    text-decoration: none;
  }
</style>