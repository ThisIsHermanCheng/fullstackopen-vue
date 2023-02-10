<script setup>
import LoginView from "./views/Login/LoginView.vue";
import LogoutView from "./views/Logout/LogoutView.vue";
import BlogView from "./views/Blog/BlogView.vue";
import blogService from "./services/blogs";
import { ref } from "vue";

const user = ref(JSON.parse(window.localStorage.getItem("loginedUser")));
if (user.value) blogService.setToken(user.value.token);
</script>

<template>
  <div v-if="!user">
    Login to application
    <LoginView @setUser="(u) => (user = u)" />
  </div>
  <div v-else>
    <LogoutView @removeUser="user = null" />
    welcome {{ user.username }}
    <BlogView :userId="user.id" />
  </div>
</template>
