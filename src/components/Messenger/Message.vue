<template>
  <div v-if="isCurrentUser" class="message-card message-card-current">
    <!-- <span class="username">{{message.user}}</span>  -->
    <span class="username">You</span> 
    <span class="message message-current">{{ message.body }}</span>
  </div>

  <div v-else class="message-card">
    <span class="username">{{ message.user }}</span> 
    <span class="message">{{ message.body }}</span>
  </div>

</template>

<script>

export default {
  props: [
    'user',
    'message'
    ],
    computed: {
      isCurrentUser() {
        return this.message.user === this.user
      }
    }
}
</script>


<style scoped>
  .message-card {
    display: flex;
    flex-direction: column-reverse;
    padding: 10px 4px;
    margin-bottom: 10px;
    font-family: sans-serif;
    align-items: flex-start;
  }
  .message-card-current {
    align-self: right;
    align-items: flex-end;
  }
  .username{
    color: #999;
    font-size: .7em;
    /* padding-left: 15px; */
  }
  .message {
    border: 2px solid #007bff;
    background-color: #007bff;
    color: #fff;
    border-radius: 8px;
    padding: 10px;
    font-weight: bold;
  }
  .message-current {
    background-color: #28a745;
    border-color: #28a745;
    color: white;
  }
</style>
