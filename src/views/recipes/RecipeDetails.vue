<template>
  <div id="recipe-details">
      <div v-if="recipe"><br>
        <h1>{{ recipe.title }}</h1><br>
        <img :src="recipe.images.medium" alt="medium image"><br><br>
        <h2>{{ recipe.description }}</h2><br>
        <p>Date Posted: {{ recipe.postDate }}</p>
        <p>Date Edited: {{ recipe.editDate }}</p><br>
        <p>Servings: {{ recipe.servings }}</p>
        <p>Prep Time: {{ recipe.prepTime }} mins</p>
        <p>Cook Time: {{ recipe.cookTime }} mins</p><br>
        <h3>Ingredients:</h3><br>
        <div v-for="ingredient in recipe.ingredients" :key="ingredient.uuid">
          <p>{{ ingredient.amount }} {{ ingredient.measurement }} {{ ingredient.name }}</p>
        </div><br>
        <h3>Directions:</h3><br>
        <div v-for="direction in recipe.directions" :key="direction.uuid">
          <p>{{ direction.instructions }}<span v-if="direction.optional"> *Optional*</span></p> 
        </div>
        <div v-if="specials"><br>
          <h3>Specials: </h3><br>
          <div v-for="special in specials" :key="special">
            <div v-for="ingredient in recipe.ingredients" :key="ingredient.uuid">
              <div v-if="special.ingredientId === ingredient.uuid">
                <p>{{ special.title }} {{ special.type }}</p>
                <p>{{ special.text }}</p><br>
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