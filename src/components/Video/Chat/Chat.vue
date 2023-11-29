<script setup>
// import ref, reactive, onMounted
import { ref, reactive, onMounted } from 'vue';

let message = ref(""); // int, string, boolean
let allMessages = reactive({
    data: [],
});

// GET request to the API for messages when component is mounted
onMounted(async () => {
    try {
        const response = await fetch('https://nodejs-messages.onrender.com/api/v1/messages');
        const data = await response.json();

        if (data.status === 'success') {
            // update the local messages data with the received messages
            allMessages.data = data.data[0].messages;
        } else {
            console.error('Failed to fetch messages:', data.message);
        }
    } catch (error) {
        console.error('Error fetching messages:', error.message);
    }
});


// function sendMessage
const sendMessage = () => {
    allMessages.data.push(message.value);
    message.value = "";
};

</script>

<template>
    <div>
        <ul>
            <li v-for="m in allMessages.data" :key="m._id">
                {{ m.user }}: {{ m.message }}
            </li>
        </ul>

        <div>
            <input v-model="message" type="text" placeholder="">
            <button @click="sendMessage">Send</button>
        </div>
    </div>
</template>

<style scoped></style>