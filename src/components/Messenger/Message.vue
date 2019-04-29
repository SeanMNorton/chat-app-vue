<template>
  <div class="message-card">
    <span class="username">{{ message.user }}:</span> 
    <span class="message">{{ message.body }}</span>
  </div>
</template>

<script>

export default {
  props: [
    'username', 
    'message'
    ], 
}
</script>


<style scoped>
  .message-card {
    padding: 4px 0px;
    font-family: sans-serif;
  }
  .username{
    color: #777
  }
  .message {
    margin-left: 8px;
    color: #333;
    font-weight: bold;
  }
</style>
