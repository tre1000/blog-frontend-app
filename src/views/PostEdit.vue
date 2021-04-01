<template>
  <div id="post-edit">
    <form v-on:submit.prevent="updatePost(post)">
      <h1>Update a post</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="post.title" />
      </div>
      <div class="form-group">
        <label>Image Url:</label>
        <input type="text" class="form-control" v-model="post.image" />
      </div>
      <div class="form-group">
        <label>Body:</label>
        <input type="text" class="form-control" v-model="post.body" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
// info is not displaying in text boxes
// it also doesn't work
export default {
  data: function () {
    return {
      post: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("api/posts/" + this.$route.params.id).then((response) => {
      console.log(response);
      this.post = response;
    });
  },
  methods: {
    updatePost: function (post) {
      var params = {
        title: post.title,
        image: post.image,
        body: post.body,
      };
      axios
        .patch("api/posts/" + this.$route.params.id, params)
        .then(() => {
          this.$router.push("/recipes/" + this.recipe.id);
        })
        .catch((errors) => console.log(errors.data));
    },
  },
};
</script>
