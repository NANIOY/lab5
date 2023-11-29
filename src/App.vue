<script setup>
  import VideoPlayer from './components/Video/VideoPlayer.vue';
  import VideoDetails from './components/Video/VideoDetails.vue';
  import Chat from './components/Video/Chat/Chat.vue';

  import { ref } from 'vue';
  let newDescription = ref("Default title");

  const updateVideo =  (description) => {
    newDescription.value = description;
  };

</script>

<template>
  <div class="tiktok">
    <div>
      <VideoPlayer @update:video-description="updateVideo"/>
    </div>

    <div>
      <VideoDetails :description="newDescription"/>
      <Chat />
    </div>

  </div>
</template>

<style scoped>
  .tiktok {
    display: grid;
    grid-template-columns: 0.5fr 1fr;
  }
</style>