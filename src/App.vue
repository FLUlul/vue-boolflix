<template>
  <div id="app">
    <Header
    @sendMovieData="getMovieData"
    @sendTvData="getTvData"
    />

    <main>

    <Movies
    :importMovieData="savedMovieData"
    :importTvData="savedTvData"
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
      savedMovieData: [],
      savedTvData: [],
    }
  },

  methods: {
    getMovieData(data){
      this.savedMovieData = data
      console.log("array movie:", this.savedMovieData);
    },
    getTvData(data){
      this.savedTvData = data
      console.log("array tv:", this.savedTvData);
    }
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
