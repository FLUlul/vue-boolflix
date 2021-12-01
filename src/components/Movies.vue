<template>
  <section>
    <ul v-for="movie, i in importData" :key="i">
      <li>Title: {{movie.title}}</li>
      <li>Original Title: {{movie.original_title}}</li>
      <li>Language: <img :src="require(`../assets/flags/${movie.original_language}.png`)" :alt="movie.original_language"> </li>
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
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  section{
    display: flex;
    flex-wrap: wrap;
    padding: 20px 0;

    ul{
      border: solid black 2px;
      padding: 10px;
      margin: 5px 10px;
      list-style: none;
      color: white;
      width: calc(100% / 4 - 20px);
    }
  }
</style>
