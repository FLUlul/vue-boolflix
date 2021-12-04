<template>
  <section>

    <Cards
    :DataArray="importMovieData"
    :Type="'Movie'"
    />

    <Cards
    :DataArray="importTvData"
    :Type="'Series'"
    />

  </section>
</template>

<script>
import axios from 'axios'
import Cards from '@/components/Cards.vue'

export default {
  
  name: 'Movies',

  components: {
    Cards,
  },

  props: {
    importInput: String,
  },

  data(){
    return {
      urimovie: 'https://api.themoviedb.org/3/search/movie',
      uritv: 'https://api.themoviedb.org/3/search/tv',
      apikey: '?api_key=8e1d397aa3a246f7489f89325ede261e',
      apiquery: '&query=',

      importMovieData: [],
      importTvData: [],
    }
  },
  /* "watch" works when "somethingToWatch" change do {that} */
  watch: {
    importInput(){

      if (this.importInput !== '') {
        axios
        .get (this.urimovie + this.apikey + this.apiquery + this.importInput)
        .then ((result) => {
          this.importMovieData = result.data.results
        })
        .catch((error) => {
        console.log(error);
        })

        axios
        .get (this.uritv + this.apikey + this.apiquery + this.importInput)
        .then ((result) => {
          this.importTvData = result.data.results
        })
        .catch((error) => {
        console.log(error);
        })
      } 
    }
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
