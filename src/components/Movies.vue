<template>
  <section>

    <Cards
    :dataArray="movieData"
    :Type="'Movie'"
    />

    <Cards
    :dataArray="tvData"
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

      movieData: [],
      tvData: [],
    }
  },
  /* "watch" works when "somethingToWatch" change do {that} */
  watch: {
    importInput(){

      if (this.importInput !== '') {
        /* axios movies call */
        axios
        .get (this.urimovie + this.apikey + this.apiquery + this.importInput)
        .then ((result) => {
          this.movieData = result.data.results
          
          this.movieData.forEach((element) => {
            axios
            .get ('https://api.themoviedb.org/3/movie/' + element.id + '/credits' + this.apikey)
            .then ((result) => {

              if (result.data.cast.length > 5) {
                result.data.cast.length = 5
              }
              //the array cast is created inside the object movie
              //element.cast = result.data.cast;
              this.$set(element, 'cast', result.data.cast)
            })
            .catch((error) => {
            console.log(error);
            })
          })
        })
        .catch((error) => {
        console.log(error);
        })
        
        /* axios tv series call */
        axios
        .get (this.uritv + this.apikey + this.apiquery + this.importInput)
        .then ((result) => {
          this.tvData = result.data.results

          this.tvData.forEach((element) => {
            axios
            .get ('https://api.themoviedb.org/3/tv/' + element.id + '/credits' + this.apikey)
            .then ((result) => {

              if (result.data.cast.length > 5) {
                result.data.cast.length = 5
              }
              //the array cast is inserted inside the object movie, creating a brand new key 'cast'
              //element.cast = result.data.cast;
              this.$set(element, 'cast', result.data.cast)
            })
            .catch((error) => {
            console.log(error);
            })
          })
        })
        .catch((error) => {
        console.log(error);
        })

      } 
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
