<template>
  <div class="page">
    <div 
      :style="styles" 
      v-chat-scroll="{always: false, smooth: true}" 
      class="messages-container">
      <div class="messages" v-for="(message, index) in messages" :key="index">
        <p>
          <span class="username">{{ message.user }}:</span> 
          <span class="text">{{ message.text }}</span>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import io from 'socket.io-client';

export default {
  props: ['styles'],
  data() {
    return {
      messages: [ ],
      socket : io(process.env.VUE_APP_SOCKET_IO_URL)
    }
  },
  mounted() {
    this.socket.on('MESSAGE', (data) => {
        this.messages = [...this.messages, data];
    });
  },
}
</script>


<style scoped>
  .messages-container {
    overflow: scroll;
    position: fixed;
    padding: 20px 10px;
    bottom: 10vh;
    width: 100vw;
    font-size: 1.2em;
    box-sizing: border-box;
  }
  .messages {
    font-family: sans-serif
  }
  .username{
    color: #777
  }
  .text {
    color: #333;
    font-weight: bold;
    margin-left: 8px;
  }
</style>