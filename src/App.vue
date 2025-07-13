<template>
  <div id="app">
    <div>
      {{message}}
    </div>

    <div id="app-2">
      <span v-bind:title="message2">
        鼠标悬停几秒钟查看此处动态绑定的提示信息！
      </span>
    </div>

    <div id="app-5">
      <button v-on:click="reverseMessage">反转消息</button>
    </div>

    <div id="app-6">
      <p>message</p>
      <input v-model="message">
    </div>
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'App',
  data() {
    return {
      message: 'Hello Vue!',
      message2: '页面加载于 ' + new Date().toLocaleString()
    }
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  },
  components: {
    HelloWorld
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
