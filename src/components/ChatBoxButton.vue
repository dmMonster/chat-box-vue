<template>
    <transition name="chat-box-rotate">
        <div v-on:click="showChatBox = !showChatBox" class="chat-box-button" v-if="showChatBox" v-bind:key="1">
            <i class="fas fa-comment fa-3x"></i>
        </div>
        <div v-on:click="showChatBox = !showChatBox" class="chat-box-button" v-else v-bind:key="2">
            <i class="fas fa-window-close fa-3x"></i>
        </div>
    </transition>

</template>

<script>
    export default {
        name: "ChatBoxButton",
        data() {
            return {
                showChatBox: true,
            }
        },
        watch: {
            showChatBox: function () {
                this.$emit("show-chat-box");
            }
        }
    }
</script>


<style scoped lang="scss">
    .chat-box-button {
        position: fixed;
        right: 5px;
        bottom: 5px;
        background-color: transparent;
        cursor: pointer;
        padding: 1em;
    }

    .chat-box-button:hover {
        background-color: #1b4bd2;
        border-radius: 50%;
        color: white;
    }

    .chat-box-rotate-enter-active, .chat-box-rotate-leave-active {
        transition: all 1s ease;
    }
    .chat-box-rotate, .chat-box-rotate-leave-to
        /* .component-fade-leave-active below version 2.1.8 */ {
        transform: rotate(40deg);
    }
</style>