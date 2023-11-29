<script setup>
//define props
const props = defineProps(['description']);
</script>

<template>
  <div class="user">
    <img src="https://i.imgur.com/ExsMDsS.png" alt="user image">
    <div class="username">
      <h3>sami2bx</h3>
      <h4>Sami Something</h4>
    </div>
  </div>

  <p>{{ description }}</p>
</template>

<style scoped>

</style>