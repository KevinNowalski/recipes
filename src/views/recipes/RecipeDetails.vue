<template>
  <div v-if="recipe">
    <h1>{{ recipe.title }}</h1>
    <p>{{ recipe.description }}</p>
  </div>
  <div v-else>
    <p>Loading recipe details... </p>
  </div>
   
</template>

<script>
export default {
  props: ['id'],
   data() {
    return {
      recipe: null
    }
  },
  mounted() {
    fetch('http://localhost:3001/recipes/' + this.id)
      .then(res => res.json())
      .then(data => this.recipe = data)
      .catch(err => console.log(err.message))
  }
}
</script>

<style>

</style>