<template>
  <div class="IndexPosts">
    <h1>{{ message }}</h1>
    <div v-for="post in posts" v-bind:key="post.id">
      <router-link v-bind:to="`posts/${post.id}`">
        <h2>{{ post.title }}</h2>
        <img v-bind:src="post.image" v-bind:alt="post.title" />
      </router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Posts",
      posts: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/api/posts").then((response) => {
        this.posts = response.data;
      });
    },
  },
};
</script>
