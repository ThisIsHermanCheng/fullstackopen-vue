<template>
  <button @click="deleteRecord">Delete</button>
</template>

<script setup>
import blogService from "../../services/blogs";
import { defineProps } from "vue";
const props = defineProps({
  blogId: {
    type: String,
    required: true,
  },
});
const emit = defineEmits(["onDelete"]);

function deleteRecord() {
  blogService.deleteRecord(props.blogId).then(() => emit("onDelete"));
}
</script>
