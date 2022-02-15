<script setup>
import UserCard from "./components/UserCard.vue";
import { onMounted, reactive } from "vue";

const state = reactive({
  user: {},
  loading: false,
  error: null,
});

onMounted(() => {
  state.loading = true;
  fetch("https://randomuser.me/api")
    .then((response) => response.json())
    .then((data) => {
      state.user = data.results[0];
    })
    .catch((error) => {
      state.error = error;
    })
    .finally(() => {
      state.loading = false;
    });
});
</script>

<template>
  <UserCard :user="state.user" :loading="state.loading" :error="state.error" />
</template>

<style>
#app {
  margin: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  background: #0f0c29;
  background: -webkit-linear-gradient(to right, #24243e, #302b63, #0f0c29);
  background: linear-gradient(to right, #24243e, #302b63, #0f0c29);
}
</style>
