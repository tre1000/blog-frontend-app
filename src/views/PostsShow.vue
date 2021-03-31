<template>
  <div id="posts-show">
    <h1>{{ post.title }}</h1>
    <img v-bind:src="post.image" v-bind:alt="post.title" />
    <p>{{ post.body }}</p>
    <router-link v-bind:to="`/posts/${post.id}/edit`">
      <button>Update post</button>
    </router-link>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    this.showPost();
  },
  methods: {
    showPost: function () {
      axios.get("/api/posts/" + this.$route.params.id).then((response) => {
        console.log(response.data);
        this.post = response.data;
      });
    },
  },
};
</script>
