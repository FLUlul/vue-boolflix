<template>
  <div id="app">

    <Header
    @sendInput="getInput"
    />

    <main>

    <Main
    :importInput="savedInput"
    />

    </main>

  </div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'

export default {
  name: 'App',

  components: {
    Header,
    Main,
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
  background-color: #141414;
  height: 100vh;
  overflow-y: auto;
}
</style>
