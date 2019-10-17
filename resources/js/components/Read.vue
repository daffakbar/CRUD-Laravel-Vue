<template>
    <div class="card">
        <div class="card-header">
            <router-link to="/"><i class="fa fa-arrow-left"></i></router-link>
        </div>
        <div class="card-body">
            <h2><u>Title</u></h2>
            <h3>{{posts.title}}</h3>
            <hr>
            <h4><u>Description</u></h4>
            <p>{{posts.description}}</p>
        </div>
    </div>
</template>
<script>
// import axios from 'axios';

export default {
  data() {
    return {
      posts: [],
      errors: []
    }
  },

  created() {
    let id = this.$route.params.id

    axios.get('/posts/' + id)
    .then(response => { 
      console.log(response.data);  
      this.posts = response.data;
    })
    .catch(e => {
      this.errors.push(e)
    })
 
  
  }
}
</script>