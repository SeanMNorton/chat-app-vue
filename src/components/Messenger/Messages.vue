<template>
    <div :class="`messages-container ${isHalfScreen ? 'half-screen' : 'full-screen'}`">
      <div class="messages" v-for="(message, index) in messages" :key="index">
        <Message :user="currentUser" :message="message"/>
      </div>
    </div>
</template>

<script>
import io from 'socket.io-client';
import Message from './Message';

export default {
  props: ['isHalfScreen', 'currentUser'],
  components: {
    Message,
  },
  data() {
    return {
      messages: [ ],
      socket : io(process.env.VUE_APP_SOCKET_IO_URL)
    }
  },
  mounted() {
    this.socket.on('MESSAGE', (data) => {
        this.messages = [data, ...this.messages];
    });
  },
}
</script>


<style scoped>
  .messages-container {
    position: fixed;
    bottom: 10vh;
    display: flex;
    flex-direction: column-reverse;
    overflow: scroll;
    width: 100vw;
    padding: 20px 10px;
    box-sizing: border-box;
    font-size: 1.2em;
  }
  .half-screen {
    height: 40vh;
  }
  .full-screen {
    height: 90vh;
  }
  .messages {
    position: relative;
    bottom: 0;
  }
</style>