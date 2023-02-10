<template>
  <div>
    <button @click="newBlogToggle = !newBlogToggle" v-if="!newBlogToggle">
      New Blog
    </button>
    <div v-else>
      <form @submit.prevent="createBlog">
        <label>title:</label>
        <input type="text" v-model="blog.title" /><br />
        <label>author:</label>
        <input type="text" v-model="blog.author" /><br />
        <label>url:</label>
        <input type="text" v-model="blog.url" /><br />
        <input type="submit" value="Submit" />
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";
import blogService from "../../services/blogs";

const emit = defineEmits(["onRefetchBlogs"]);

const newBlogToggle = ref(false);
const initialBlog = {
  title: "",
  author: "",
  url: "",
};
const blog = reactive({ ...initialBlog });

async function createBlog() {
  blogService.create(blog).then(() => {
    emit("onRefetchBlogs");
    Object.assign(blog, initialBlog);
  });
}
</script>
