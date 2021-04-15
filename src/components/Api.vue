<template>
  <div id="app">
    <h2>Posts Json Placeholder</h2>
    <div v-if="! posts.length">
      <p>
        Chargement des posts…
      </p>
    </div>
    <div v-else>
        <table>
            <tr>
                <th>Title</th>
                <th>Id</th>
                <th>Id de l'utilisateur</th>
                <th>Description</th>
            </tr>
            <tr v-for="post in posts" :key="post.id">
                <td>{{ post.title[0].toUpperCase() + post.title.substring(1) }}</td>
                <td>{{ post.id }}</td>
                <td>{{ post.userId }}</td>
                <td>{{ post.body }}</td>
            </tr>
        </table>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'SimpleVue',
  data() {
    return {
      posts: [],
    }
  },
  mounted() {
    axios.get('https://jsonplaceholder.typicode.com/posts?' + new URLSearchParams({
        _limit: 10
    }))
      .then(res => {
        this.posts = res.data
      })
     .catch(error => console.error(error))
  },
  methods: {
      updateResource(data){
        this.posts = data
      }
  },
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 35rem;
  margin: 0 auto;
}
.article {
  list-style: none;
  padding-left: 0;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
</style>