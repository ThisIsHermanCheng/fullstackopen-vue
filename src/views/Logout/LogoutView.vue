<template>
  <div>
    <button @click="logout">Logout</button>
  </div>
</template>

<script setup>
const emit = defineEmits(["removeUser"]);
function logout() {
  window.localStorage.removeItem("loginedUser");
  emit("removeUser", {});
}
</script>

<style lang="scss" scoped></style>
