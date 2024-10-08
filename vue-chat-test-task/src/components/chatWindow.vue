<template>
  <div class="chat-window">
    <h2>{{ user }}</h2>
    <div class="message-list">
      <div
        v-for="(msg, index) in messages"
        :key="index"
        :class="['message', { self: msg.user === user }]"
      >
        <div class="message-content">
          <strong>{{ msg.user }}:</strong> {{ msg.message }}
          <small class="timestamp">{{ msg.timestamp }}</small>
        </div>
      </div>
    </div>
    <div class="input-container">
      <input
        v-model="newMessage"
        placeholder="Напишите сообщение"
        @keyup.enter="sendMessage"
      />
      <button @click="sendMessage">Отправить</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

// Пропсы
const props = defineProps({
  user: String,
  messages: Array,
});

// Локальное состояние для ввода нового сообщения
const newMessage = ref("");

// Отправка сообщения
const emit = defineEmits(["sendMessage"]);
const sendMessage = () => {
  if (newMessage.value.trim() !== "") {
    emit("sendMessage", props.user, newMessage.value);
    newMessage.value = ""; // Очистка поля ввода
  }
};
</script>

<style scoped>
.chat-window {
  width: 300px;
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 5px;
  background-color: #f9f9f9;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.message-list {
  height: 300px;
  overflow-y: auto;
  margin-bottom: 10px;
  border: 1px solid #eee;
  padding: 10px;
  border-radius: 5px;
  background-color: #fff;
}

.message {
  margin-bottom: 10px;
  padding: 5px;
  border-radius: 5px;
  display: flex;
  justify-content: flex-start;
  text-align: left;
}

.message.self {
  justify-content: flex-end;
  text-align: right;
}

.message-content {
  max-width: 70%;
  padding: 5px;
  border-radius: 5px;
  background-color: #e0e0e0;
  display: inline-block;
}

.message.self .message-content {
  background-color: #dcf8c6;
}

.timestamp {
  display: block;
  font-size: 10px;
  margin-top: 2px;
  color: #777;
}

.input-container {
  display: flex;
}

input {
  flex: 1;
  padding: 5px;
  border-radius: 5px 0 0 5px;
  border: 1px solid #ccc;
}

button {
  padding: 5px 10px;
  border: none;
  background-color: #4caf50;
  color: white;
  border-radius: 0 5px 5px 0;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}
</style>
