<template>
  <div id="app">
    <Messages :styles=MessageContainerStyle />
    <Form :onFocus=handleInputFocus />
  </div>
</template>

<script>
import Messages from './components/Messenger/Messages.vue';
import Form from './components/Messenger/Form.vue';

export default {
  name: 'app',
  data() {
    return {
      MessageContainerStyle: 'height: 79vh;'
    }
  },
  components: {
    Form,
    Messages,
  },
  methods: {
    isMobile() { return /iPhone|iPad|iPod|Android/i.test(navigator.userAgent) },
    handleInputFocus(size) {
      if (this.isMobile()) {
        this.MessageContainerStyle = `height: ${size === 'full' ? '79':'42'}vh;`
      }
    }
  },
  mounted() {
    if (!this.isMobile()) {
      this.MessageContainerStyle = 'height: 90vh';
    }
  }
}
</script>

<style>
  body, html {
    margin: 0;
    padding: 0;
    overflow: hidden;
  }
</style>