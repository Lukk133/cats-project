<template >
  <div class="container">
    
      <div v-for="post in posts" :key="post.id">
        <div> {{ post.entry_number }} {{ post.pokemon_species.name }}</div>
        
      </div>
    </div>
  
  <!--<div :hidden="hideData"></div>-->
  
</template>
<script>
import axios from 'axios'


export default {
  name: 'HomeView',
  components: {
  },
  data() {
    return {
      hideData: true,
      posts: [],
      task: '',
      tasks: [
        {
          name: 'Peter'
        }],
    }
  },
  created() {
    /*można też mounted*/
    axios
      .get(`https://pokeapi.co/api/v2/pokedex/2`)
      .then((response) => {
        console.log(response.data);
        this.posts = response.data.pokemon_entries
      })
  }
}



</script>

