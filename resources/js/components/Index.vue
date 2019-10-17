<template>
    <div class="card">
        <div class="card-header">
            <router-link to="./Create" class="btn btn-primary float-sm-right">Create</router-link>
        </div>
        <div class="card-body">
            <table class="table table-bordered">
                <thead>
                    <tr>
                        <th>Title</th>
                        <th>Description</th>
                        <th></th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(post, index) in posts" :key="post.id">
                        <td>{{post.title}}</td>
                        <td>{{post.description}}</td>
                        <td>
                            <router-link :to="{ name: 'read', params: { id: post.id }}" class="btn btn-success"><i class="fa fa-eye"></i> View</router-link>
                            <router-link :to="{ name: 'edit', params: { id: post.id }}" class="btn btn-warning"><i class="fa fa-pencil-alt"></i> Edit</router-link>
                            <button v-on:click="submitPostdelete(post.id, index)" class="btn btn-danger"><i class="fa fa-trash"></i> Delete</button>
                            <!-- <router-link class="btn btn-danger"><i class="fa fa-trash"></i> Delete</router-link> -->
                        </td>
                    </tr>
                </tbody>
            </table>
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
    axios.get('/posts')
    .then(response => { 
    //   console.log(response.data);  
      this.posts = response.data;
    })
    .catch(e => {
      this.errors.push(e)
    })
 
  
  },
  methods: {
    
  
  submitPostdelete(id, index) {
    if (confirm("Click 'Ok' to delete.")){
    axios.delete(`/posts/`+ id)
    .then(response => {
        console.log(response)
        this.posts.splice(index, id)
      // JSON responses are automatically parsed.
      // this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
  }
  }
}
</script>