<template>
  <div id="cards">

    <div class="card" v-for="object, i in DataArray" :key="i">
      
      <div>
        <img src="https://hesolutions.com.pk/wp-content/uploads/2019/01/picture-not-available.jpg" alt="no image" v-if="object.poster_path === null">
        <img :src="`https://image.tmdb.org/t/p/w342/${object.poster_path}`" :alt="object.title" v-else>
      </div>
      
      <ul>
        <li><span>Title: </span>{{object.title}}</li>
        <li><span>Original Title: </span>{{object.original_title}}</li>
        <li><span>Language: </span><img :src="require(`../assets/flags/${changeFlag(object.original_language)}.png`)" :alt="object.original_language"></li>
        <li>

          <span>
            Vote: 
          </span>

          <span v-for="star, index in voteArr" :key="'B' + index" >

            <i v-if="transformVote(object.vote_average) > index" class="fas fa-star"></i>
            <i v-else class="far fa-star"></i>
            
          </span>

        </li>
        <li><span>Overview: </span> {{object.overview}}</li>
        <li><span>Cast: </span>{{object.id}}</li>
      </ul>

      <div class="tag">{{Type}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Cards',

  props: {
    DataArray: Array,
    Type: String
  },

  data(){
    return {
      newVote: 0,
      voteArr: [1,2,3,4,5],
    }
  },

  methods: {
    changeFlag(flag){
      if(flag == 'it'){
        return "it"
      }else if(flag == 'en'){
        return "en"
      }else{
        return "eu"
      }
    },

    transformVote(vote){
      return parseInt(Math.round(this.newVote = vote / 2))
    },

  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import '~@fortawesome/fontawesome-free/css/all.min.css';

  #cards{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    padding: 20px 0;  
  }

  .card{
    max-width: 342px;
    margin: 5px 10px;
    color: white;
    background-color: black;
    border: solid white 2px;
    position: relative;
    overflow: hidden;

    .tag{
      position: absolute;
      top: 5px;
      right: 5px;
      background-color: black;
      padding: 1px 2px;
      border-radius: 5px;
    }

    .poster {
      height: 100%;
      display: flex;
      align-items: center;

      img{
        max-width: 100%;
      }
    } 
    
    &:hover ul{
      background-color: black;
      display: block;
    }

    ul{
      list-style: none;
      width: 100%;
      height: 100%;
      position: absolute;
      top: 0;
      left: 0;
      display: none;
      z-index: 10;
      padding: 10px;
      overflow-y: auto;
  
      span {
        font-weight: 700;
      }
    }
  }
</style>