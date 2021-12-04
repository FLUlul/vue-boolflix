<template>
  <div id="app">
    <Header
    @sendMovieData="getMovieData"
    @sendTvData="getTvData"
    :importCastId="savedId"
    />

    <main>

    <Movies
    :importMovieData="savedMovieData"
    :importTvData="savedTvData"
    @sendCastId="getCastId"
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
      savedId: 0,
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
    },
    getCastId(id){
      this.savedId = id
      console.log("saved id", this.savedId);
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
