
<template>
  <Header />
  <RouterView />
</template>
<script setup>
import { RouterView } from 'vue-router'
import Header from '@/components/Header.vue'

</script>
<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100;400&display=swap');


* {
  font-family: 'Roboto', sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  max-width: 1100px;
  margin: 0 auto;
}
</style>
