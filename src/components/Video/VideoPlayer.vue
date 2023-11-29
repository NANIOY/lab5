<script setup>
    import { ref , reactive, onMounted} from 'vue';

    //define emits
    const emit = defineEmits('update:videoDescription');

    const videoUrl = ref("");
    let videos = reactive({
        data: [],
    });

    onMounted(() => {
        fetch("https://api.jsonbin.io/v3/b/6548ef9954105e766fcc2c15")
            .then((response) => response.json())
            .then((data) => {
                console.log(data);
                videos.data = data.record.videos;
                videoUrl.value = videos.data[0].video;

                //emit videoDescription
                emit('update:videoDescription', videos.data[0].description);

            });
    });

</script>

<template>
    <video :src="videoUrl" controls autoplay muted></video>
</template>

<style scoped>
    video {
        width: 512px;
        height: auto;
    }
</style>