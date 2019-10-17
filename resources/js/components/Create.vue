<template>
    <div class="card">
        <div class="card-header">
            <h2>Create New Post</h2>
        </div>

        <div class="card-body">
            <form v-on:submit="submitPost()">
                <div class="form-group">
                    <input type="text" v-model="posts.title" id="" class="form-control" placeholder="Title...">
                </div>
                <div class="form-group">
                    <textarea rows="4" type="text" v-model="posts.description" id="" class="form-control"
                        placeholder="Desription"> </textarea>
                </div>
                <div class="form-group">
                    <router-link to="./" class="btn btn-warning">Cancel</router-link>
                    <button type="submit" class="btn btn-primary">Submit</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
// import axios from 'axios';

export default {
  data: function() {
    return {
      posts: {
          title: '',
          description: ''
      },
      errors: []
    }
  },
methods:{


  // Fetches posts when the component is created.
  submitPost() {
    axios.post(`/posts`, this.posts)
    .then(response => {
        console.log(response)

        this.$router.push({path:'/'})

      // JSON responses are automatically parsed.
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
  }
}
</script>