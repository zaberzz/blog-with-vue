<template>
  <div class="home">
    <h1>home</h1>
    <div v-if="error">{{ error }}</div>
    <div v-if="posts.length">
      <PostList :posts="posts" /> <TagCloud :posts="posts"></TagCloud>
    </div>
    <div v-else><Spinner /></div>
  </div>
</template>

<script>
import TagCloud from "@/components/TagCloud.vue";
import PostList from "../components/PostList.vue";
import getPosts from "../composable/getPsts";
import Spinner from "@/composable/Spinner.vue";
export default {
  name: "HomeView",
  components: { PostList, Spinner, TagCloud },
  setup() {
    const { posts, error, load } = getPosts();
    load();
    return { posts, error };
  },
};
</script>
