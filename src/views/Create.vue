<template>
  <div class="create">
    <form @submit.prevent="submitHandler">
      <lable>Title</lable>
      <input v-model="title" type="text" required />
      <label>Content:</label>
      <textarea v-model="body" required></textarea>
      <label>Tags(for adding tags press enter)</label>
      <input v-model="tag" type="text" @keydown.enter.prevent="handleKeydown" />
      <div class="pill" v-for="tag in tags" :key="tag">#{{ tag }}</div>
      <button>Add post</button>
    </form>
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";
import { useRouter } from "vue-router";
export default {
  setup() {
    const title = ref("");
    const body = ref("");
    const tag = ref("");
    const tags = ref([]);
    const router = useRouter;

    const handleKeydown = () => {
      if (!tags.value.includes(tag.value)) {
        tag.value.replace(/\s/, "");
        tags.value.push(tag.value);
      }
      tag.value = "";
    };
    const submitHandler = async () => {
      const post = {
        title: title.value,
        body: body.value,
        tag: tag.value,
      };
      await fetch(" http://localhost:3000/posts", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(post),
      });
      router.push({ name: "Home" });
    };
    return { title, body, tag, tags, handleKeydown, submitHandler };
  },
};
</script>

<style></style>
