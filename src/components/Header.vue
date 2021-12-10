<template>
  <header>

    <div>
      <img src="../assets/boolflix-logo.png" alt="boolflix-logo">
    </div>

    <nav>
      <input type="text" v-model.trim="inputUser" @keydown.enter="saveInput">

      <button @click.prevent="saveInput">Search</button>
    </nav>

  </header>
</template>

<script>

export default {
  name: 'Header',

  data(){
    return {
      inputUser: "",
      inputSaved: "",
    }
  },

  methods: {
    saveInput(){
      this.inputSaved = this.inputUser
      this.$emit('sendInput', this.inputSaved)
      this.inputUser = ""
    }
  }
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
    
    div {
      width: 150px;
      cursor: pointer;
      img {
        max-width: 100%;
      }
    }
  }
</style>
