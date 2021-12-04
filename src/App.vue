<template>
  <div id="app">

    <Header
    @sendInput="getInput"
    />

    <main>

    <Movies
    :importInput="savedInput"
    />

    </main>

  </div>
</template>

<script>
import Header from './components/Header.vue'
import Movies from './components/Movies.vue'

export default {
  name: 'App',

  components: {
    Header,
    Movies,
  },

  data(){
    return {
      savedInput: "",
    }
  },

  methods: {
    getInput(input){
      this.savedInput = input
    },
  }
}
</script>

<style lang="scss">
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: grey;
  height: 100vh;
  overflow-y: auto;
}
</style>
