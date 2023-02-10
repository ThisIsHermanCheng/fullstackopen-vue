<template>
  <div>
    {{ props.blog.title }}
    <button @click="hidden = !hidden">
      {{ hidden ? "show" : "hide" }}
    </button>
    <br />
    <div v-if="!hidden">
      {{ blogLikes }}
      <BlogLike
        :blogId="props.blog.id"
        :blogLikes="blogLikes"
        @onLike="blogLikes++"
      />
      <br />
      {{ props.blog.author }}
      <br />
      <BlogDelete
        v-if="userId === props.blog.user.id"
        :blogId="props.blog.id"
        @onDelete="emit('onRefetchBlogs')"
      />
    </div>
  </div>
</template>

<script setup>
import { defineProps, ref } from "vue";
import BlogLike from "./BlogLike.vue";
import BlogDelete from "./BlogDelete.vue";
const emit = defineEmits(["onRefetchBlogs"]);

const props = defineProps({
  blog: Object,
  userId: String,
});
const hidden = ref(true);
const blogLikes = ref(props.blog.likes);
</script>
