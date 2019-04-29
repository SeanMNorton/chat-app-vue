<template>
  <div id="app">
    <Messages :currentUser="currentUser" :isHalfScreen="isKeyboardShowing"/>
    <Form :updateCurrentUser="updateCurrentUser" :inputFocus='updateInput' />
  </div>
</template>

<script>
import Messages from './components/Messenger/Messages.vue';
import Form from './components/Messenger/Form.vue';

export default {
  name: 'app',
  data() {
    return {
      currentUser: '',
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
    },
    updateCurrentUser(name) {
      this.currentUser = name;
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
    height: unset;
    overflow: hidden !important;
  }
</style>