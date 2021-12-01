<template>
  <section>
    <ul v-for="movie, i in importData" :key="i">
      <li>Title: {{movie.title}}</li>
      <li>Original Title: {{movie.original_title}}</li>
      <li>Language: {{movie.original_language}}</li>
      <li>Vote: {{movie.vote_average}}</li>
    </ul>
  </section>
</template>

<script>


export default {
  name: 'Movies',

  props: {
    importData: Array,
  },

  data() {
    return {
      
    }
  },

  methods: {
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  section{
    display: flex;
    flex-wrap: wrap;

    ul{
      border: solid black 2px;
      padding: 10px;
      margin: 5px 10px;
      list-style: none;
      color: white;
    }
  }
</style>
