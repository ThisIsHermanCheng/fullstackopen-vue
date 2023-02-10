<template>
  <form @submit.prevent="userLogin">
    <label>Username:</label><br />
    <input type="text" v-model="user.username" /><br />
    <label>Password:</label><br />
    <input type="text" v-model="user.password" /><br /><br />
    <input type="submit" value="Submit" />
  </form>
</template>

<script setup>
import users from "../../services/users";
import blogService from "../../services/blogs";
import { reactive } from "vue";

const emit = defineEmits(["setUser"]);

const user = reactive({
  username: "",
  password: "",
});

async function userLogin() {
  const loginedUser = await users.login(user);
  window.localStorage.setItem("loginedUser", JSON.stringify(loginedUser));
  blogService.setToken(loginedUser.token);
  emit("setUser", loginedUser);
}
</script>
