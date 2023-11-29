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
.user {
  display: flex;
  align-items: center;
  margin-bottom: 1em;
}

img {
  width: 3em;
  height: 3em;
  border-radius: 50%;
  margin-right: 0.5em;
}
.username {
  display: flex;
  flex-direction: column;
}

h3 {
  font-size: 1.4em;
  font-weight: 500;
}

h4 {
  font-size: 0.9em;
  margin-top: -1.2em;
  font-weight: 300;
}

p {
  font-size: 1em;
  margin-top: -1.2em;
  margin-bottom: 2em;
  font-weight: 300;
}
</style>