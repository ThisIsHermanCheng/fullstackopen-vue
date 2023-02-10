<template>
  <BlogCreateView @onRefetchBlogs="fetchBlogs" />
  <div
    v-for="blog in blogs"
    :key="blog.id"
    class="my-3 border-2 border-spacing-1 w-96"
  >
    <BlogItem
      :blog="blog"
      @onRefetchBlogs="fetchBlogs"
      :userId="props.userId"
    />
  </div>
</template>

<script setup>
import blogService from "../../services/blogs";
import BlogItem from "./BlogItem.vue";
import BlogCreateView from "./BlogCreateView.vue";
import { ref, defineProps } from "vue";
const props = defineProps({
  userId: {
    type: String,
    required: true,
  },
});
const blogs = ref([]);
function fetchBlogs() {
  blogService.getAll().then((b) => (blogs.value = b));
}
fetchBlogs();
</script>
