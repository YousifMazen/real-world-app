<template>
  <div>
    <h1>{{ post.title }}</h1>
    <h6>By: {{ post.userId }}</h6>
    <p>
      {{ post.body }}
    </p>
  </div>
</template>
<script>
export default {
  props: ["id"],

  data() {
    return {
      post: {},
    };
  },

  mounted() {
    const postId = this.$route.params.id;
    this.fetchPost(postId);
  },

  methods: {
    fetchPost(postId) {
      fetch(`https://jsonplaceholder.typicode.com/posts/${postId}`)
        .then((response) => {
          if (!response.ok) {
            throw new Error(`HTTP error! Status: ${response.status}`);
          }
          return response.json();
        })
        .then((data) => {
          this.post = data;
        })
        .catch((error) => {
          console.error("Error fetching post: ", error);
        });
    },
  },
};
</script>
<style></style>
