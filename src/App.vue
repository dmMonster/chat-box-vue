<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <ChatBox v-if="chatBoxVisibility"/>
    <ChatBoxButton v-on:show-chat-box="showChatBox"  />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ChatBoxButton from "@/components/ChatBoxButton";
import ChatBox from "@/components/ChatBox";


export default {
  name: 'App',
  components: {
    ChatBox,
    ChatBoxButton,
    HelloWorld
  },
  data() {
    return {
      chatBoxVisibility: false,
    }
  },
  methods: {
    showChatBox: function() {
      this.chatBoxVisibility = !this.chatBoxVisibility;
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
