<template>
    <div v-if="username.length > 2" class="form-container">
        <form @submit.prevent="sendMessage">
            <div class="form-group">
                <input 
                    @focus="onFocus('half')"
                    @blur="onFocus('full')"
                    type="text" 
                    v-model="message" 
                    placeholder="Message"
                >
                <button type="submit">Send</button>
            </div>
        </form>
    </div> 

    <div v-else class="form-container">
        <form @submit.prevent="submitName">
            <div class="form-group user">
                <input 
                    @focus="onFocus('half')"
                    @blur="onFocus('full')"
                    type="text" 
                    v-model="user" 
                    placeholder="UserName"
                >
                <button type="submit">new user</button>
            </div>
        </form>
    </div> 
</template>


<script>
import io from 'socket.io-client';

export default {
    props: ['onFocus'],
    data() {
        return {
            user: '',
            username: '',
            message: '',
            socket : io(process.env.VUE_APP_SOCKET_IO_URL)
        }
    },
    methods: {
        sendMessage() {
            this.socket.emit('SEND_MESSAGE', {
                user: this.username,
                text: this.message
            });
            this.message = ''
        },
        submitName() {
            this.username = this.user;
            this.user = '';
        }
    },
}
</script>

<style>
    .form-container {
        height: 10vh;
        position: fixed;
        bottom: 0;
        width: 100vw;
        background: lightblue;
    }
    form {
        display: flex;
        flex-direction: column;
        align-items: center;
        flex-wrap: wrap;
    }
    .form-group {
        display: flex;
        justify-content: center;
        margin-top: 1.5vh;
        align-items: center;
    }
    input {
        height: 7vh;
        padding-left: 10px;
        outline: none;
        border: none;
        box-sizing: border-box;
        width: 75vw;
        font-size: 1em;
    }
    button {
        height: 7vh;
        font-size: 1em;
        width: 20vw;
        margin-left: 1vw;
        border: none;
        outline: none;
        background-color: black;
        color: white;
        box-sizing: border-box;
    }
    input, button {
        border-radius: 8px;
    }
</style>
