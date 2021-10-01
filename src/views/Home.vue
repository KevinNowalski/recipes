<template>
  <div class="home"><br>
    <h1>Recipes Home</h1><br>
    <p>The Recipes App pulls data from the API.  It creates a list view which includes all the recipes.  It also creates a recipe detail view to display each recipe.  The Ingredients with a matching ingredientId listed in the specials response should also show the special title, type and text under the ingredient name</p><br>
    <router-link to="/recipes" class="recipe"><h2>Go to recipes</h2></router-link>
  </div>
</template>

<script>
export default {
  name: 'Home',
  components: { }
}
</script>
