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
import Cards from '@/components/Cards.vue'

export default {
  
  name: 'Movies',

  components: {
    Cards,
  },

  props: {
    importMovieData: Array,
    importTvData: Array,
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
