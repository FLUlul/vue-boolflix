<template>
    <div id="filter">

      <span>Genres: </span>

      <select name="genres-list" id="genres" v-model="genreValue" @change="$emit('changeIt', genreValue)">
        
        <option value="All">All</option>

        <option v-for="genre in genresArray" :key="genre.id" :value="genre.id">{{genre.name}}</option>

      </select>

    </div>
</template>

<script>

export default {
  name: 'Genres',

  props: {
    genresArray: Array
  },

  data(){
    return{
      genreValue: 'All'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  #filter{
    margin: 10px 5px;
  }
  span{
    color: white;
    font-weight: 700;
  }
</style>
