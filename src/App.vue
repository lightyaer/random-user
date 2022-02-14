<script setup>
import UserCard from "./components/UserCard.vue";
import { onMounted, reactive } from "vue";

const state = reactive({
  user: {},
});

onMounted(() => {
  fetch("https://randomuser.me/api")
    .then((response) => response.json())
    .then((data) => {
      state.user = data.results[0];
    });
});
</script>

<template>
  <UserCard :user="state.user" />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
