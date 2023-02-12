<script setup>
import { RouterView } from 'vue-router'
import PageHeader from './components/Header.vue';
</script>

<template>
  <PageHeader/>
  <RouterView />
</template>


<script>
export default {
  name: 'App',
  components: {
    PageHeader
  }
}
</script>
