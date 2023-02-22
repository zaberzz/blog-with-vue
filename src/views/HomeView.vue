<template>
  <div class="home">
    <h1>home</h1>
    <PostList :posts="posts" />
  </div>
</template>

<script>
import PostList from "../components/PostList.vue";
import { ref } from "vue";
export default {
  name: "HomeView",
  components: { PostList },
  setup() {
    const posts = ref([
      { title: "welcome to the blog", body: "lorem", id: 1 },
      { title: "top 5 css trip", body: "lorem", id: 2 },
    ]);
    return { posts };
  },
};
</script>
