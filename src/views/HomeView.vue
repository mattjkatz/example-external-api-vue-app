<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      posts: [],
    };
  },
  created: function () {
    this.postsIndex();
    this.newsIndex();
  },
  methods: {
    postsIndex: function () {
      axios.get("https://jsonplaceholder.typicode.com/posts").then((response) => {
        console.log(response.data);
        this.posts = response.data;
      });
    },
    newsIndex: function () {
      axios.get("/news-api").then((response) => {
        console.log(response.data);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <div v-for="post in posts" v-bind:key="post.id">
      <p>{{ post }}</p>
    </div>
  </div>
</template>

<style></style>
