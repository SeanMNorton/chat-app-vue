<template>
    <!-- Username Form -->
    <div v-if="username.length < 2" class="form-container">
        <form @submit.prevent="saveName">
            <div class="form-group">
                <input type="text" v-model="name" placeholder="Username" @focus="inputFocus(true)" />
                <button type="submit">Save</button>
            </div>
        </form>
    </div> 
    <!-- Message Form  -->
    <div v-else class="form-container">
        <form @submit.prevent="sendMessage">
            <div class="form-group">
                <input 
                    id="messageInput" 
                    type="text" 
                    v-model="message" 
                    placeholder="Message"
                    @focus="inputFocus(true)"
                    @blur="inputFocus(false)" 
                />
                <button type="submit">Send</button>
            </div>
        </form>
    </div> 
</template>


<script>
import io from 'socket.io-client';

export default {
    props: ['inputFocus', 'updateCurrentUser'],
    data() {
        return {
            name: '',
            username: '',
            message: '',
            socket : io(process.env.VUE_APP_SOCKET_IO_URL)
        }
    },
    methods: {
        sendMessage() {
            if( this.message !== '' ) { 
                this.emitMessage(); 
                this.message = '';
            }
            document.getElementById('messageInput').focus();
        },
        emitMessage() {
            this.socket.emit('SEND_MESSAGE', {
                user: this.username,
                body: this.message
            });
        },
        saveName() {
            if (this.name.length > 2) {
                this.username = this.name;
                this.updateCurrentUser(this.name);
                this.name = '';
            }
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
        max-width: 650px;
        font-size: 1em;
    }
    button {
        height: 7vh;
        font-size: 1em;
        width: 20vw;
        max-width: 150px;
        margin-left: 1vw;
        border: none;
        outline: none;
        background-color: #28a745;
        color: white;
        box-sizing: border-box;
    }
    input, button {
        border-radius: 8px;
    }
</style>
