<template>
    <div class="chat-box">
        <div class="chat-box-header">
            <h4>Chat box</h4>
        </div>
        <div class="messages">
            <div v-for="message in messages" class="message" v-bind:user="message.author">
                <div class="avatar"><i class="fa fa-user-tie fa-2x"></i></div>
                <div class="message-text">{{message.message}}</div>
                <div class="time">{{message.datetime}}</div>
            </div>
        </div>
        <div class="new-message">
            <input v-on:keyup.enter="sendMessage" placeholder="Enter you message" v-model="newMessage">
            <div v-on:click="sendMessage" class="send-icon">
                <i class="fa fa-paper-plane fa-2x"></i>
            </div>
        </div>

    </div>
</template>

<script>
    export default {
        name: "ChatBox",
        data() {
            return {
                messages: "",
                currentUser: "I",
                newId: "",
                newMessage: "",
                backendSrc: "http://localhost:3000"
            }
        },
        mounted: function () {
            this.updateMessages();
        },
        methods: {
            sendMessage: async function () {

                if (this.newMessage.trim() === "") {
                    document.querySelector(".new-message>input").style.border = "1px solid red";
                    return false;
                }

                await fetch(this.backendSrc + "/messages", {
                    method: "POST",
                    headers: {
                        "Accept": "application/json",
                        "Content-Type": "application/json"
                    },
                    body: JSON.stringify({
                        "id": this.newId,
                        "author": this.currentUser,
                        "datetime": new Date().toLocaleString(),
                        "message": this.newMessage,
                    })
                });
                await this.updateMessages();
                this.newMessage = "";
            },
            updateMessages: function () {
                fetch(this.backendSrc + "/messages")
                    .then((response) => {
                        return response.json();
                    })
                    .then((response) => {
                        this.messages = response;
                        this.newId = this.messages.length + 1;
                    })
            }
        },
        watch: {
            messages: function () {
                //nextTick - waiting to v-for
                this.$nextTick(() => {
                    let messages = document.querySelector(".messages");
                    messages.scrollTo(0, messages.scrollHeight);
                })
            }
        }
    }
</script>

<style scoped lang="scss">
    .chat-box {
        position: fixed;
        right: 5px;
        bottom: 6em;
        background-color: #34495E;
        color: white;
        width: 100%;
        max-width: 500px;
        border-radius: 0 0 5px 5px;
        box-shadow: 1px 5px 50px black;
    }

    .chat-box-header {
        background-color: #455f77;
        position: absolute;
        top: 0;
        width: 100%;
        border-radius: 0 0 5px 5px;

        h4 {
            padding-top: 1em;
            margin-top: 0;
        }
    }

    .messages {
        margin-top: 1em;
        height: 500px;
        overflow-y: scroll;
    }

    .message {
        display: flex;
        background-color: #95A5A6;
        margin: 1em 1em 2em 1em;
        padding: 2em 1em 1em 1em;
        border-radius: 0 8px 8px 8px;
        flex-wrap: nowrap;
        max-width: 75%;

        .user {
            display: none;
        }

        .avatar {
            flex-grow: 1;
            height: 100%;
            text-align: left;
        }

        .message-text {
            flex-grow: 6;
            word-break: break-word;
        }

        .time {
            font-size: 50%;
        }
    }

    .new-message {
        padding: 1em;
        height: 3em;
        display: flex;
        flex-wrap: nowrap;
        align-content: center;
        align-items: center;

        input {
            text-align: center;
            border: none;
            border-radius: 5px;
            width: 100%;
            height: 100%;
            background-color: rgba(214, 198, 203, 0.2);
        }

        input:focus {
            box-shadow: 1px 1px 20px #1a243f;
        }

        .send-icon {
            cursor: pointer;
        }
    }

    div[user="I"] {
        margin: 0 3px 1em auto;
        border-radius: 8px 0 8px 8px;

        .avatar{
            display: none;
        }
    }


</style>