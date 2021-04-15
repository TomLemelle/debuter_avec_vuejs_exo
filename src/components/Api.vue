<template>
  <div id="app">
    <h2>Posts Json Placeholder</h2>
    <div v-if="! posts.length">
      <p>
        Chargement des posts…
      </p>
    </div>
    <div v-else>
      <ul>
        <li v-for="post in posts" :key="post.id">
          <h3>{{ post.title[0].toUpperCase() + post.title.substring(1) }}</h3>
            <p>Id de l'utilisateur : {{ post.userId }}</p>
            <p>Id du post : {{ post.id }}</p>
            <p>Corps du post : {{ post.body }}</p>
        </li>
      </ul>
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
    axios.get('https://jsonplaceholder.typicode.com/posts')
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

</style>