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
    var code = this.$route.query.code;
    if (code) {
      axios.get("/auth/github/callback?code=" + code).then((response) => {
        localStorage.setItem("github_access_token", response.data.access_token);
        this.$router.push("/about");
      });
    }
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
    <a href="https://github.com/login/oauth/authorize?client_id=c83a4deb9a15cb7036ea">Sign into GitHub</a>
    <div>
      <img
        src="https://media3.giphy.com/media/o0vwzuFwCGAFO/200w.gif?cid=82a1493b8h2j0r41x5lui6jxz4yrg7m4qt5zqg7umt7rm4m5&rid=200w.gif&ct=g"
        alt=""
      />
      <img src="https://c.tenor.com/58DNSt-Lvw0AAAAM/corgi-computer.gif" alt="" />
    </div>
    <div v-for="post in posts" v-bind:key="post.id">
      <h3>{{ post.title }}</h3>
      <p>{{ post.body }}</p>
    </div>
  </div>
</template>

<style></style>
