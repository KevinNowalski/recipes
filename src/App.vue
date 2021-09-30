<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link :to="{ name: 'About' }">About</router-link> |
    <router-link :to="{ name: 'Recipes' }">Recipes</router-link>
  </div>

  <button @click="redirect">Redirect</button>
  <button @click="back">Go back</button>
  <button @click="forward">Go forward</button>

  <router-view/>

</template>

<script>
export default {
  methods: {
    redirect(){
      this.$router.push({ name: 'Home' })
    },
    back(){
      this.$router.go(-1)
    },
    forward(){
      this.$router.go(1)
    }
  }
}
</script>

<style type="text/css">
*{
  box-sizing: border-box;
}

body{
  padding: 0;
  margin: 0;
  overflow-x: hidden;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000;
  width: 1000px;
  max-width: 100%;
  margin: 0 auto;
  font-size: 18px;
  padding: 30px 15px;
}

#nav {
  padding: 30px 15px;
}

#nav a {
  font-weight: bold;
  color: #000;
  text-decoration: none;
  padding: 10px;
  border-radius: 4px;
}

#nav a.router-link-exact-active {
  color: #fff;
  background: #004EFF
}
button {
  margin: 0 10px;
  padding: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
@media only screen and (max-width: 479px){
  #app{
    font-size: 16px;
  }
}
</style>
