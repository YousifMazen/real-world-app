<template>
  <h1>Blog Posts</h1>
  <label for="">Search: </label>
  <input type="text" v-model="searchTerm" />
  <ul>
    <li v-for="post in filteredPosts" :key="post.id">
      <router-link :to="{ name: 'postPage', params: { id: post.id } }">
        <h2>{{ post.title }}</h2>
      </router-link>
    </li>
    <br />
  </ul>
</template>

<script>
export default {
  data() {
    return {
      posts: [],
      searchTerm: "",
    };
  },
  mounted() {
    this.fetchPosts();
  },

  computed: {
    filteredPosts() {
      const term = this.searchTerm.toLowerCase();
      return this.posts.filter((post) =>
        post.title.toLowerCase().includes(term)
      );
    },
  },

  methods: {
    fetchPosts() {
      fetch("https://jsonplaceholder.typicode.com/posts")
        .then((response) => {
          if (!response.ok) {
            throw new Error(`HTTP error! Status: ${response.status}`);
          }
          return response.json();
        })
        .then((data) => {
          this.posts = data;
          console.log(data);
        })
        .catch((error) => {
          console.error("Error fetching posts:", error);
        });
    },
  },
};
</script>
