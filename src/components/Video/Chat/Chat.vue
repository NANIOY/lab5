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


// POST request to the API to send a message
const sendMessage = async () => {
    try {
        // create a temporary variable to hold new message
        const newMessage = {
            user: 'NANIO',
            message: message.value,
        };

        // send a POST request to the API with the message
        const response = await fetch('https://nodejs-messages.onrender.com/api/v1/messages', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(newMessage),
        });

        const responseData = await response.json(); // parse the response

        // if the response is successful, add the message to the local messages data
        if (responseData.status === 'success') {
            allMessages.data.push(newMessage); // add the message to the local messages data
            message.value = ""; // clear input field
        } else {
            console.error('Failed to send message');
        }
    } catch (error) {
        console.error('Error sending message:', error.message);
    }
};

</script>

<template>
    <div>
        <ul>
            <li class="message-item" v-for="m in allMessages.data" :key="m._id">
                <span class="user">{{ m.user }}</span>
                <span class="message">{{ m.message }}</span>
            </li>
        </ul>

        <div class="chat-input">
            <input v-model="message" type="text" placeholder="Add comment..">
            <button @click="sendMessage">Send</button>
        </div>
    </div>
</template>

<style scoped>
.chat-input {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 1em;
}

input {
    width: 100%;
    padding: 0.5em;
    border: 1px solid #ccc;
    border-radius: 5px;
}

button {
    padding: 0.5em 1em;
    border: none;
    border-radius: 5px;
    background-color: #ccc;
    color: #fff;
    cursor: pointer;
}

button:hover {
    background-color: #aaa;
}

ul {
    list-style: none;
    padding: 0;
}

.message-item {
    margin-bottom: 1em;
    display: flex;
    flex-direction: column;
    margin-bottom: 1em;
}

.user {
    font-weight: bold;
    margin-bottom: 0.2em;
    font-size: 0.9em;
}

.message {
    font-size: 0.8em;
}
</style>