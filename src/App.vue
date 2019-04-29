<template>
  <div id="app">
    <Messages :isHalfScreen="isKeyboardShowing"/>
    <Form :inputFocus='updateInput' />
  </div>
</template>

<script>
import Messages from './components/Messenger/Messages.vue';
import Form from './components/Messenger/Form.vue';

export default {
  name: 'app',
  data() {
    return {
      inputFocused: false,
    }
  },
  components: {
    Form,
    Messages,
  },
  methods: {
    isMobile() { return /iPhone|iPad|iPod|Android/i.test(navigator.userAgent) },
    updateInput(status) {
      this.inputFocused = status;
    }
  },
  computed: {
      isKeyboardShowing(){ return this.isMobile() && this.inputFocused },
  }
}
</script>

<style>
  body, html, #app {
    margin: 0;
    padding: 0;
    overflow: hidden !important;
  }
</style>