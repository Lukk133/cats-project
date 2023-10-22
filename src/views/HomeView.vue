<template >
  <div class="container">
    <div class="d-flex container">
      <input v-model="task" type="text" class="form-control" placeholder="Input a name">
      <button class="btn btn-primary" @click="search">Wyszukaj</button>
    </div>

    <div :hidden="hideData">
      <div v-for="post in posts" :key="post.id">
        <div>Name: {{ post.name }}</div>
        <div>Count: {{ post.count }}</div>
        <div>Gender: {{ post.gender }}</div>
        <div>Probability of the gender: {{ post.probability }}</div>
      </div>
    </div>
  </div>
  
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
      .get(`https://api.genderize.io?name=`)
      .then((response) => {
        console.log(response.data);
        this.posts = response
      })
  },
  methods: {
    search() {
      if (this.task.length === 0) return;

      if (this.task.length === 50) { alert('Maksymalna liczba znaków to 50') };

      this.tasks.push({
        name: this.task,
      })
      let name = this.task
      axios
        .get(`https://api.genderize.io?name=${name}`)
        .then((response) => {
          console.log(response.data);
          this.posts = response
        })
      this.task = '',
        this.hideData = false
    }
  },
}



</script>
