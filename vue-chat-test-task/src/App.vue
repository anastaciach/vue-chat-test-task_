<template>
  <div class="chat-container">
    <ChatWindow user="User 1" :messages="messages" @sendMessage="sendMessage" />
    <ChatWindow user="User 2" :messages="messages" @sendMessage="sendMessage" />
  </div>
</template>

<script setup>
import { ref } from "vue";
import ChatWindow from "./components/ChatWindow.vue";

// Реактивный массив для хранения сообщений
const messages = ref([]);

// Функция для отправки сообщений
const sendMessage = (user, message) => {
  messages.value.push({
    user,
    message,
    timestamp: new Date().toLocaleTimeString(),
  });
};
</script>

<style scoped>
.chat-container {
  display: flex;
  justify-content: space-around;
  padding: 20px;
  gap: 30px;
}
</style>
