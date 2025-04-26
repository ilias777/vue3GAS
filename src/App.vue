<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view />
</template>

<script setup></script>

<style scoped>
nav {
  padding: 1rem;
}
router-link {
  margin: 0 0.5rem;
}
</style>
