<template>
  <div id="recipe-details">
      <div v-if="recipe">
        <h1>{{ recipe.title }}</h1>
        <p>{{ recipe.description }}</p>
        <img :src="recipe.images.full" alt="full image"><br>
        <img :src="recipe.images.medium" alt="medium image"><br>
        <img :src="recipe.images.small" alt="small image">
        <p>Servings: {{ recipe.servings }}</p>
        <p>Prep Time: {{ recipe.prepTime }}</p>
        <p>Cook Time: {{ recipe.cookTime }}</p>
        <p>Post Date: {{ recipe.postDate }}</p>
        <p>Edit Date: {{ recipe.editDate }}</p>
        <h3>Ingredients:</h3>
        <div v-for="ingredient in recipe.ingredients" :key="ingredient.uuid">
          <p>UUID: {{ ingredient.uuid }}</p>
          <p>Amount: {{ ingredient.amount }}</p>
          <p>Measurement: {{ ingredient.measurement }}</p>
          <p>Name: {{ ingredient.name }}</p>
        </div>
        <h3>Directions:</h3>
        <div v-for="direction in recipe.directions" :key="direction.uuid">
          <p>Instructions:<br> {{ direction.instructions }}</p>
          <p>Optional: {{ direction.optional }}</p>
        </div>
        <div v-if="specials">
          <h3>Specials: </h3>
          <div v-for="special in specials" :key="special">
            <div v-for="ingredient in recipe.ingredients" :key="ingredient.uuid">
              <div v-if="special.ingredientId === ingredient.uuid">
                <p>Type: {{ special.type }}</p>
                <p>Title: {{ special.title }}</p>
                <p>Text: {{ special.text }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div v-else>
        <p>Loading recipe details... </p>
      </div>
  </div>
</template>

<script>
export default {
  props: ['id'],
   data() {
    return {
      recipe: null,
      specials: null,
      publicPath: process.env.BASE_URL
    }
  },
  mounted() {
    fetch('http://localhost:3001/recipes/' + this.id)
      .then(res => res.json())
      .then(data => this.recipe = data)
      .catch(err => console.log(err.message))

    fetch('http://localhost:3001/specials/')
      .then(res2 => res2.json())
      .then(data2 => this.specials = data2)
      .catch(err2 => console.log(err2.message))
  }
}
</script>

<style>
    img{
        width: 450px;
        max-width: 100%
    }
</style>