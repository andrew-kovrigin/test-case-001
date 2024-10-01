<template>
  <div id="app">
    <h1>Эмулятор двусторонней переписки</h1>
    <div class="chat-container">
      <!-- Chat for User 1 -->
      <div class="chat-box">
        <h3>Пользователь 1</h3>
        <div class="messages">
          <div v-for="(message, index) in messages" :key="index" :class="{'message-right': message.user === 'user2'}">
            <span>{{ message.user }}: {{ message.text }}</span>
          </div>
        </div>
        <input v-model="user1Message" placeholder="Введите сообщение">
        <button @click="sendMessage('user1')">Отправить</button>
      </div>

      <!-- Chat for User 2 -->
      <div class="chat-box">
        <h3>Пользователь 2</h3>
        <div class="messages">
          <div v-for="(message, index) in messages" :key="index" :class="{'message-left': message.user === 'user1'}">
            <span>{{ message.user }}: {{ message.text }}</span>
          </div>
        </div>
        <input v-model="user2Message" placeholder="Введите сообщение">
        <button @click="sendMessage('user2')">Отправить</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const messages = ref([]);
    const user1Message = ref('');
    const user2Message = ref('');

    const sendMessage = (user) => {
      if (user === 'user1' && user1Message.value.trim() !== '') {
        messages.value.push({ user: 'user1', text: user1Message.value });
        user1Message.value = '';
      } else if (user === 'user2' && user2Message.value.trim() !== '') {
        messages.value.push({ user: 'user2', text: user2Message.value });
        user2Message.value = '';
      }
    };

    return {
      messages,
      user1Message,
      user2Message,
      sendMessage,
    };
  },
};
</script>

<style>
.chat-container {
  display: flex;
  justify-content: space-between;
  padding: 20px;
}
.chat-box {
  width: 45%;
  border: 1px solid #ccc;
  padding: 10px;
}
.messages {
  margin-bottom: 10px;
  height: 200px;
  overflow-y: auto;
}
.message-right {
  text-align: right;
}
.message-left {
  text-align: left;
}
</style>
