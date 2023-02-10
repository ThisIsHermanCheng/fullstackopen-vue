<template>
  <button @click="like">Like</button>
</template>

<script setup>
import blogService from "../../services/blogs";
import { defineProps } from "vue";
const props = defineProps({
  blogId: {
    type: String,
    required: true,
  },
  blogLikes: {
    type: Number,
    required: true,
  },
});
const emit = defineEmits(["onLike"]);

function like() {
  blogService
    .update(props.blogId, { likes: props.blogLikes + 1 })
    .then(() => emit("onLike"));
}
</script>
