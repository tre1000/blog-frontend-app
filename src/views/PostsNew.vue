<template>
  <div class="posts-new">
    <form v-on:submit.prevent="createPost()">
      <h1>Create a post</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="title" />
      </div>
      <div class="form-group">
        <label>Image Url:</label>
        <input type="text" class="form-control" v-model="image" />
      </div>
      <div class="form-group">
        <label>Body:</label>
        <input type="text" class="form-control" v-model="body" />
        <small v-if="body.length > 0 && body.length < 200">{{ 1000 - body.length }} characters left</small>
      </div>
      <!-- this button isn't doing anything for whatever reason. -->
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      title: "",
      body: "",
      image: "",
    };
  },
  created: function () {},
  methods: {
    createPost: function () {
      var params = {
        title: this.title,
        body: this.body,
        image: this.image,
      };
      axios
        .post("/api/posts", params)
        .then((response) => {
          console.log("Post added!", response.data);
          this.$router.push("/posts");
        })
        .catch((error) => console.log(error.response.data));
    },
  },
};
</script>
