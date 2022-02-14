<script setup>
import { defineProps } from "vue";

const { user } = defineProps(["user"]);
</script>

<template>
  <p>Hi</p>
  <div v-if="user">
    <p>{{ user.email }}</p>
  </div>
</template>

<style scoped>
a {
  color: #42b983;
}
</style>
