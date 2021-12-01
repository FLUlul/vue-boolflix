<template>
  <header>

    <div>
      <h1>BOOLFLIX</h1>
    </div>

    <nav>
      <input type="text" v-model.trim="inputSearch" @keydown.enter="requestAPI">

      <button @click.prevent="requestAPI">Search</button>
    </nav>

  </header>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Header',
  data(){
    return {
      inputSearch: "",
      savedInp: "",

      urimovie: 'https://api.themoviedb.org/3/search/movie?',
      uritv: 'https://api.themoviedb.org/3/search/tv?',
      apikey: 'api_key=8e1d397aa3a246f7489f89325ede261e',
      apiquery: '&query=',

      dataSearch: [],
    }
  },
  methods: {
    axiosCall(uri){
      axios
      .get (uri + this.apikey + this.apiquery + this.savedInp)
      .then ((result) => {

        this.dataSearch = result.data.results

        /* console.log(this.dataSearch, this.apiquery, this.savedInp); */
        this.$emit('sendData', this.dataSearch)

        this.inputSearch = ""
        
      })
      .catch((error) => {
      console.log(error);
      })
    },

    requestAPI() {
      this.savedInp = this.inputSearch

      if(this.savedInp !== ""){
        this.axiosCall(this.urimovie)

        this.axiosCall(this.uritv)
      }
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: black;
    padding: 10px;
    
    div{
      color: red;
    }
  }
</style>
